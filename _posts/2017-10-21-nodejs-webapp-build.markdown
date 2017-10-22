---
layout: post
title:  "NodeJS web 工程构建"
date:   2017-10-21 00:26:00 +0800
categories: code
---

nodejs 工程构建（参考：https://expressjs.com/en/starter/installing.html）

一、通过node和npm构建

	1. $ mkdir myapp
	2. $ cd myapp
	3. $ npm init -- set config(notice the entry point filename)
	4. $ npm install express --save/----no-save (add it to the dependencies list or not)
	5. add code to entry poin file
		const express = require('express')
		const app = express()
		app.get('/', function (req, res) {
  			res.send('Hello World!')
		})
		app.listen(3000, function () {
  			console.log('Example app listening on port 3000!')
		})
	6. $ node app.js

二、通过 express 构建器构建

	1. $ npm install express-generator -g —— 安装构建器
	2. $ express --view=pug myapp —— 生成项目工程，名称是myapp
	3. $ cd myapp
	4. $ npm install —— 安装依赖
	5. $ DEBUG=myapp:* npm start —— 启动