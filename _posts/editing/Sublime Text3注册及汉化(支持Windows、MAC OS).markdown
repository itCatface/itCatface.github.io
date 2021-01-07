# 注册

- 各操作系统hosts文件目录

		windows：c:/windows/system32/drivers/etc/hosts
		linux：/etc/hosts
		mac：/Private/etc

## 版本-v3211
1. hosts文件文末换行追加

		127.0.0.1 www.sublimetext.com
		127.0.0.1 sublimetext.com
		127.0.0.1 sublimehq.com
		127.0.0.1 license.sublimehq.com
		127.0.0.1 45.55.255.55
		127.0.0.1 45.55.41.223
		0.0.0.0 license.sublimehq.com
		0.0.0.0 45.55.255.55
		0.0.0.0 45.55.41.223

2. 注册码

		----- BEGIN LICENSE -----
		Member J2TeaM
		Single User License
		EA7E-1011316
		D7DA350E 1B8B0760 972F8B60 F3E64036
		B9B4E234 F356F38F 0AD1E3B7 0E9C5FAD
		FA0A2ABE 25F65BD8 D51458E5 3923CE80
		87428428 79079A01 AA69F319 A1AF29A4
		A684C2DC 0B1583D4 19CBD290 217618CD
		5653E0A0 BACE3948 BB2EE45E 422D2C87
		DD9AF44B 99C49590 D2DBDEE1 75860FD2
		8C8BB2AD B2ECE5A4 EFC08AF2 25A9B864
		------ END LICENSE ------​


## 版本-v3176

1. hosts文件文末换行追加
	
		127.0.0.1       www.sublimetext.com
		127.0.0.1       license.sublimehq.com

2. 注册码

		----- BEGIN LICENSE -----
		sgbteam
		Single User License
		EA7E-1153259
		8891CBB9 F1513E4F 1A3405C1 A865D53F
		115F202E 7B91AB2D 0D2A40ED 352B269B
		76E84F0B CD69BFC7 59F2DFEF E267328F
		215652A3 E88F9D8F 4C38E3BA 5B2DAAE4
		969624E7 DC9CD4D5 717FB40C 1B9738CF
		20B3C4F1 E917B5B3 87C38D9C ACCE7DD8
		5F7EF854 86B9743C FADC04AA FB0DA5C0
		F913BE58 42FEA319 F954EFDD AE881E0B
		------ END LICENSE ------

## 版本-v3103及以上
- 仅需输入注册码

		—– BEGIN LICENSE —–
		Ryan Clark
		Single User License
		EA7E-812479
		2158A7DE B690A7A3 8EC04710 006A5EEB
		34E77CA3 9C82C81F 0DB6371B 79704E6F
		93F36655 B031503A 03257CCC 01B20F60
		D304FA8D B1B4F0AF 8A76C7BA 0FA94D55
		56D46BCE 5237A341 CD837F30 4D60772D
		349B1179 A996F826 90CDB73C 24D41245
		FD032C30 AD5E7241 4EAA66ED 167D91FB
		55896B16 EA125C81 F550AF6B A6820916
		—— END LICENSE ——


## 版本-v3103以下

- 仅需输入注册码

		----- BEGIN LICENSE -----
		Andrew Weber
		Single User License
		EA7E-855605
		813A03DD 5E4AD9E6 6C0EEB94 BC99798F
		942194A6 02396E98 E62C9979 4BB979FE
		91424C9D A45400BF F6747D88 2FB88078
		90F5CC94 1CDC92DC 8457107A F151657B
		1D22E383 A997F016 42397640 33F41CFC
		E1D0AE85 A0BBD039 0E9C8D55 E1B89D5D
		5CDB7036 E56DE1C0 EFCC0840 650CD3A6
		B98FC99C 8FAC73EE D2B95564 DF450523
		------ END LICENSE ------


# 汉化

1. **打开 View > Show Console 输入以下文本后 Enter 安装 Package Control，完成后重启 Sublime Text.**
	- **Sublime Text3** 

		```
		import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
		```
	- **Sublime Text2**
	
		```
		import urllib2,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
		```

2. **点击 Preferences > Package Control 输入 Install Package，等待片刻再输入 ChineseLocalization 安装即可.**

3. **效果如下.**

	![这里写图片描述](https://img-blog.csdnimg.cn/img_convert/8575e9eb3089081d3d28449cd12101ee.png)

	**Windows(上) &&& MAC OS(下)**

	![这里写图片描述](https://img-blog.csdnimg.cn/img_convert/544f342043c286d67a65f5d5f782aebe.png)


	