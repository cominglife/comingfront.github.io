---
layout: post
title: 收藏本页与设置首页功能，兼容ie、firefox，不兼容chrome
category: "note"
tags: ["css"]
---

收藏本页功能，兼容ie、firefox，不兼容chrome：

	<a href="javascript:AddFavorite(window.location.href,document.title);">收藏</a>

	<script language="javascript">
		function AddFavorite(sURL,sTitle){
			try{
				window.external.addFavorite(sURL, sTitle);
			}
			catch(e){
				try{
					window.sidebar.addPanel(sTitle, sURL, "");
				}
				catch(e){
					alert("加入收藏失败，请使用Ctrl+D进行添加");
				}
			}
		}
	<script>

设为首页功能：

	function setHomepage() {
		if(document.all) {
			document.body.style.behavior = 'url(#default#homepage)';
			document.body.setHomePage(window.location.href);
		}else if(window.sidebar) {
			if(window.netscape) {
				try{
					netscape.security.PrivilegeManager.enablePrivilege("UniversalXPConnect");
				}catch(e){
					alert("该操作被浏览器拒绝，如果想启用该功能，请在地址栏内输入 about:config ，然后将项 signed.applets.codebase_principal_support 值该为 true 。");
				}
			}
			var prefs = Components.classes['@mozilla.org/preferences-service;1'].getService(Components.interfaces.nsIPrefBranch);
			prefs.setCharPref('browser.startup.homepage',window.location.href);
		}
	}
















