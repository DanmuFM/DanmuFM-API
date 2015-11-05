#弹幕电台 API 说明文档

##API 基础格式


### URL
http://danmu.fm/x/?action/arg0/arg1&a=1&b=2



##歌曲

http://danmu.fm/x/?song/{sid}

	GET //返回单曲

	RETURN
		{
			sid, //歌曲唯一 SID
			uid, //提交用户 UID
			title, //歌曲标题
			url, //歌曲原始详细页地址 （虾米，网易云，QQ音乐）
			img, //封面图地址
			album_name, //专辑名称
			artist_name, //专辑演唱者名称
			text, //简介文字
			src, //歌曲可用地址 （虾米特有）
			length, //歌曲时长 （秒）
			created, //创建时间 （10位时间戳）
			modified //最后修改时间 （10位时间戳）
		}


	POST //提交歌曲（需登录状态）需登录
		{
			title, //歌曲标题
			url, //歌曲原始详细页地址 （虾米，网易云，QQ音乐）
			img, //封面图地址
			album_name, //专辑名称
			artist_name, //专辑演唱者名称
			text, //简介文字
			src, //歌曲可用地址 （虾米特有）
			length, //歌曲时长 （秒）
		}

	RETURN
		{
			sid, //歌曲唯一 SID
			uid, //提交用户 UID
			title, //歌曲标题
			url, //歌曲原始详细页地址 （虾米，网易云，QQ音乐）
			img, //封面图地址
			album_name, //专辑名称
			artist_name, //专辑演唱者名称
			text, //简介文字
			src, //歌曲可用地址 （虾米特有）
			length, //歌曲时长 （秒）
			created, //创建时间 （10位时间戳）
			modified //最后修改时间 （10位时间戳）
		}
	

	DELETE //删除歌曲 需判断权限


	PUT //修改歌曲信息 需判断权限
		{
			内容同 POST，无需更改部分无需提交
		}



##精选集 

http://danmu.fm/x/?collect/{cid}   //唯一 ID

	GET //请求精选集

	RETURN
		{
			cid, //精选集 id
			uid, //用户 id
			title, //精选集标题
			text, //精选集简介文字
			img, //精选集封面图
			num, //精选集歌曲数量
			follow, //关注人数
			look, //查看数
			created, // 创建时间戳
			modified // 修改时间戳
		}
 

 	POST //新建精选集
		{
			title /^.{1,50}$/, //精选集 标题
			text /^.{5,100}$/, // 精选集简介文字
			url // 精选集来源（可选）
		}

	RETURN
		{
			//上同
		}


##搜索


http://danmu.fm/x/?search/{text} 

	GET

	RETURN
		{
			sid,
			aid,
			mid,
			uid,
			title,
			url,
			img,
			album_name,
			artist_name,
			length,
			text,
			src,
			created,
			modified
		}


##喜欢

http://danmu.fm/x/?like
	
	POST
		{
			uid'=>'/^\d+$/', //用户 UID
			'sid'=>'/^\d+$/', //歌曲 SID or 精选集 CID or 评论 cmid
			'text'=>'/^.{5,100}$/', // 说明文字
			'second // 秒数
		}


##电台 随机

http://danmu.fm/x/?rand

	GET

	RETURN 
		[
			{
				sid, //歌曲唯一 SID
				uid, //提交用户 UID
				title, //歌曲标题
				url, //歌曲原始详细页地址 （虾米，网易云，QQ音乐）
				img, //封面图地址
				album_name, //专辑名称
				artist_name, //专辑演唱者名称
				text, //简介文字
				src, //歌曲可用地址 （虾米特有）
				length, //歌曲时长 （秒）
				created, //创建时间 （10位时间戳）
				modified //最后修改时间 （10位时间戳）
			},
			…
		]

##用户

http://danmu.fm/x/?user/{uid}

	GET //获取用户信息

	RETURN
		{
			uid,
			name,
			avatar,
			look
		}


##登录、注册部分
	登录和注册部分比较特别，使用的 api.mouto.org 的 SSO 登录，需要跳转或通过 ajax 跨域请求 到 api.mouto.org/login.html
	获取登录状态 通过获取到的 sss 在后端进行登录确认