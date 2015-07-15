---
layout: post
title: JavaScript 图片的上传前预览（兼容pc端所有浏览器）
category: "note"
tags: ["JavaScript"]
---

今天偶然在网上看到一篇文章，是介绍用js实现的图片上传前预览功能的，号称兼容所有浏览器。我之前做过这个功能，由于技术能力有限，只能做到用绝对路径去预览图片。但这只有一些很旧的浏览器才支持（如ie6），新的浏览器由于安全问题已经不再支持绝对路径显示图片，之后就没研究做下去了。这篇文章居然说能做到兼容所有浏览器，非常厉害，代码如下：（注意：本文前面部分都是一些错误代码列举，想看最终成品请直接翻到最后。）

	<style type="text/css">
	#preview,.img,img{width:200px;height:200px;}
	#preview{border:1px solid #000;}
	</style>
	<div id="preview"></div>
	<input type="file" onchange="preview(this)" />
	<script type="text/javascript">
	function preview(file) {
	    var prevDiv = document.getElementById('preview');
	    if(file.files && file.files[0]) {
	        var reader = new FileReader();
	        reader.onload = function(evt){
	            prevDiv.innerHTML = '<img src="' + evt.target.result + '" />';
	        }
	        reader.readAsDataURL(file.files[0]);
	    }else{
	        prevDiv.innerHTML = '<div class="img" style="filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale,src=\'' + file.value + '\'"></div>';
	    }
	}
	</script>

代码很简单，其实现要点是：对于 Chrome、Firefox、IE10、Opera 等最新的浏览器使用 FileReader 对象来实现；对于 IE6~9 使用滤镜 filter:progid:DXImageTransform.Microsoft.AlphaImageLoader 来实现。

经过测试，这个号称这么牛B的代码实际上只兼容 ie6、ie7、ie10、firefox、chrome、opera、android，并不兼容 ie8、ie9，也没有 JS 报错（点击查看demo）。有点小失望，但按照其实现的要点来说应该是没有问题的啊，是什么原因导致不兼容 ie8、ie9 呢？

百度搜索了一上 ie9 下的 js 实现上传图片预览功能，又发现另外一段代码：

	<style type="text/css">
	#kk{width:400px;height:400px;overflow: hidden;}
	#preview_wrapper{width:300px;height:300px;background-color:#ccc;overflow: hidden;}
	#preview_fake{filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale);width:300px;overflow: hidden;}
	#preview_size_fake{filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=image);width:300px;visibility:hidden;overflow:hidden;}
	#preview{width:300px;height:300px;overflow:hidden;}
	</style>
	<script type="text/javascript">
	function onUploadImgChange(sender) { 
	    if( !sender.value.match( /.jpg|.gif|.png|.bmp/i ) ){
	        alert('图片格式无效！');
	        return false; 
	    }
	    var objPreview = document.getElementById('preview');
	    var objPreviewFake = document.getElementById('preview_fake');
	    var objPreviewSizeFake = document.getElementById('preview_size_fake');
	    if( sender.files && sender.files[0]) {
	        objPreview.style.display = 'block';
	        objPreview.style.width = 'auto';
	        objPreview.style.height = 'auto';
	        objPreview.src = sender.files[0].getAsDataURL();
	    }else if( objPreviewFake.filters) {
	        sender.select();
	        sender.blur();
	        var imgSrc = document.selection.createRange().text; 
	        objPreviewFake.filters.item('DXImageTransform.Microsoft.AlphaImageLoader').src = imgSrc; 
	        objPreviewSizeFake.filters.item('DXImageTransform.Microsoft.AlphaImageLoader').src = imgSrc; 
	        alert("已成功选择图片！");
	        autoSizePreview( objPreviewFake,objPreviewSizeFake.offsetWidth,objPreviewSizeFake.offsetHeight);
	        objPreview.style.display = 'none';
	    }
	}
	function onPreviewLoad(sender) {
	    autoSizePreview( sender, sender.offsetWidth, sender.offsetHeight );
	}
	function autoSizePreview( objPre, originalWidth, originalHeight ) {
	    var zoomParam = clacImgZoomParam( 300, 300, originalWidth, originalHeight ); 
	    objPre.style.width = zoomParam.width + 'px';
	    objPre.style.height = zoomParam.height + 'px';
	    objPre.style.marginTop = zoomParam.top + 'px';
	    objPre.style.marginLeft = zoomParam.left + 'px';
	}
	function clacImgZoomParam(maxWidth, maxHeight, width, height) {
	    var param = { width:width, height:height, top:0, left:0 };
	    if( width>maxWidth || height>maxHeight ) {
	        rateWidth = width / maxWidth; 
	        rateHeight = height / maxHeight;
	        if( rateWidth > rateHeight ) {
	            param.width = maxWidth;
	            param.height = height / rateWidth;
	        }else{
	            param.width = width / rateHeight;
	            param.height = maxHeight;
	        }
	    }
	    param.left = (maxWidth - param.width) / 2;
	    param.top = (maxHeight - param.height) / 2;
	    return param;
	} 
	</script>
	<div style="width:1000px;margin:0 auto;">
	    <input name="localfile" type="file" id="localfile" size="28" onchange="onUploadImgChange(this)"/>
	    <div id="kk">
	        <div id="preview_wrapper">
	            <div id="preview_fake">
	                <img id="preview" src="" onload="onPreviewLoad(this)"/>
	            </div>
	        </div>
	        <img id="preview_size_fake" />
	    </div>
	</div>

这段代码功能比较复杂但也比较完善，带有等比例缩小放大图片功能。经过测试与第一段代码相反，兼容 ie6、ie7、ie8、ie9 等较旧的浏览器，不兼容 ie10、firefox、chrome、opera、android 等较新的浏览器。在较新的器上有 JS 报错，错误在上面所示下划线处（点击查看demo）。对比了一下 2 段代码，其实它们的实现原理是一样的，只是两边在不同的地方出现了问题。这好办，两边互补一下就好了。

把第二段代码中兼容新浏览器部分移到第一段代码中，如下：

	<div style="width:1000px;margin:0 auto;">
	<style type="text/css">
	#preview,.img,img{width:200px;height:200px;}
	#preview{border:1px solid #000;}
	</style>
	<div id="preview"></div>
	<input type="file" onchange="preview(this)" />
	<script type="text/javascript">
	function preview(file) {
	    var prevDiv = document.getElementById('preview');
	    if(file.files && file.files[0]) {
	        var reader = new FileReader();
	        reader.onload = function(evt) {
	            prevDiv.innerHTML = '<img src="' + evt.target.result + '" />';
	        }
	        reader.readAsDataURL(file.files[0]);
	    }else{
	        file.select();
	        file.blur();
	        var imgSrc = document.selection.createRange().text; 
	        prevDiv.innerHTML = '<div class="img" style="filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale,src=\'' + imgSrc + '\'"></div>';
	    }
	}
	</script>
	</div>

经测试，改过的第一段代码已经兼容：ie6、ie7、ie10、firefox、chrome、opera、android 等所有主流浏览器了（点击查看demo）。但这段代码没有等比例缩图功能，接着把第一段代码中兼容旧浏览器部分移到第二段代码中，如下：

	<style type="text/css">
	#kk{width:400px;height:400px;overflow: hidden;}
	#preview_wrapper{width:300px;height:300px;background-color:#ccc;overflow:hidden;}
	#preview_fake{filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale);width:300px;overflow:hidden;}
	#preview_size_fake{filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=image);width:300px;visibility:hidden;overflow:hidden;}
	#preview{width:300px;height:300px;overflow:hidden;}
	</style>
	<script type="text/javascript">
	function onUploadImgChange(sender) { 
	    if( !sender.value.match( /.jpg|.gif|.png|.bmp/i ) ){
	        alert('图片格式无效！');
	        return false; 
	    }
	    var objPreview = document.getElementById('preview');
	    var objPreviewFake = document.getElementById('preview_fake');
	    var objPreviewSizeFake = document.getElementById('preview_size_fake');
	    if( sender.files && sender.files[0]) {
	        objPreview.style.display = 'block';
	        objPreview.style.width = 'auto';
	        objPreview.style.height = 'auto'; 
	        var reader = new FileReader();
	        reader.onload = function(evt) {
	            objPreview.src = evt.target.result;
	        }
	        reader.readAsDataURL(sender.files[0]);
	    }else if( objPreviewFake.filters) { 
	        sender.select();
	        sender.blur();
	        var imgSrc = document.selection.createRange().text; 
	        objPreviewFake.filters.item('DXImageTransform.Microsoft.AlphaImageLoader').src = imgSrc; 
	        objPreviewSizeFake.filters.item('DXImageTransform.Microsoft.AlphaImageLoader').src = imgSrc; 
	        alert("已成功选择图片！");
	        autoSizePreview( objPreviewFake,objPreviewSizeFake.offsetWidth,	objPreviewSizeFake.offsetHeight );
	        objPreview.style.display = 'none';
	    }
	}
	function onPreviewLoad(sender) {
	    autoSizePreview( sender, sender.offsetWidth, sender.offsetHeight );
	}
	function autoSizePreview( objPre, originalWidth, originalHeight ) {
	    var zoomParam = clacImgZoomParam( 300, 300, originalWidth, originalHeight ); 
	    objPre.style.width = zoomParam.width + 'px'; 
	    objPre.style.height = zoomParam.height + 'px'; 
	    objPre.style.marginTop = zoomParam.top + 'px';
	    objPre.style.marginLeft = zoomParam.left + 'px';
	}
	function clacImgZoomParam(maxWidth, maxHeight, width, height) {
	    var param = { width:width, height:height, top:0, left:0 };
	    if( width>maxWidth || height>maxHeight ) {
	        rateWidth = width / maxWidth;
	        rateHeight = height / maxHeight;
	        if( rateWidth > rateHeight ) {
	            param.width = maxWidth;
	            param.height = height / rateWidth;
	        }else{
	            param.width = width / rateHeight;
	            param.height = maxHeight;
	        }
	    }
	    param.left = (maxWidth - param.width) / 2;
	    param.top = (maxHeight - param.height) / 2;
	    return param;
	}
	</script>
	<div style="width:1000px;margin:0 auto;">
	    <input name="localfile" type="file" id="localfile" size="28" onchange="onUploadImgChange(this)"/>
	    <div id="kk">
	        <div id="preview_wrapper">
	            <div id="preview_fake">
	                <img id="preview" src="" onload="onPreviewLoad(this)"/>
	            </div>
	        </div>
	        <img id="preview_size_fake" />
	    </div>
	</div>

好了，经测试，上同这段代码同样兼容：ie6、ie7、ie10、firefox、chrome、opera、android、safari 等所有主流浏览器了（点击查看demo），同时还具有等比例缩图功能。但是代码稍显复杂，不方便重复使用。

好吧，我再改进一下，让代码看起来简单一点，最后得出以下代码：

	<style type="text/css">
	#preview{width:300px;height:300px;border:1px solid #000;overflow:hidden;}
	</style>
	<div style="width:1000px;margin:0 auto;">
	    <div id="preview"></div>
	    <input type="file" onchange="preview(this)" />
	</div>
	<script type="text/javascript">
	function preview(file) {
	    var prevDiv = document.getElementById('preview');
	    if(file.files && file.files[0]) {
	        var reader = new FileReader();
	        reader.onload = function(evt) {
	            prevDiv.innerHTML = '<img src="' + evt.target.result + '"  onload="onPreviewLoad(this)" />';
	        }
	        reader.readAsDataURL(file.files[0]);
	    }else{
	        file.select();
	        file.blur();
	        var imgSrc = document.selection.createRange().text;
	        prevDiv.innerHTML = '<div id="preDiv" class="img" style="filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale,src=\'' + imgSrc + '\'"></div><img id="preImg" style="filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=image,src=\''+imgSrc+'\');width:1px;visibility:hidden;overflow:hidden;" />';
	        var objPreviewSizeFake = document.getElementById("preImg");
	        var objPreviewFake = document.getElementById("preDiv");
	        setTimeout(function() {autoSizePreview(objPreviewFake,objPreviewSizeFake.offsetWidth,objPreviewSizeFake.offsetHeight);},300);
	    }
	}

	function onPreviewLoad(sender) {
	    autoSizePreview(sender,sender.offsetWidth,sender.offsetHeight);
	}

	function autoSizePreview(objPre,originalWidth,originalHeight) {
	    var zoomParam = clacImgZoomParam(300,300,originalWidth,originalHeight);
	    objPre.style.width = zoomParam.width + 'px';
	    objPre.style.height = zoomParam.height + 'px';
	    objPre.style.marginTop = zoomParam.top + 'px';
	    objPre.style.marginLeft = zoomParam.left + 'px';
	}

	function clacImgZoomParam(maxWidth,maxHeight,width,height) {
	    var param = {width:width,height:height,top:0,left:0};
	    if(width>maxWidth || height>maxHeight) {
	        rateWidth = width / maxWidth;
	        rateHeight = height / maxHeight;
	        if(rateWidth > rateHeight) {
	            param.width = maxWidth;
	            param.height = height / rateWidth;
	        }else{
	            param.width = width / rateHeight;
	            param.height = maxHeight;
	        }
	    }
	    param.left = (maxWidth - param.width) / 2;
	    param.top = (maxHeight - param.height) / 2;
	    return param;
	}
	</script>

请看下划线的数字部分，这个数字的值越小，代码不正常工作的机率越大，这里可能与电脑的硬件配制有关。我测试了我的电脑在200左右基本都能正常工作，所以我设置到了300就比较安全了，应该大部分电脑在这个数值下都会比较安全。但为了以防万一，我再改一下，得出最后的结论代码：

	<style type="text/css">
	#preview{width:300px;height:300px;border:1px solid #000;overflow:hidden;}
	</style>
	<div style="width:1000px;margin:0 auto;">
		<div id="preview"></div>
		<input type="file" onchange="preview(this)" />
	</div>
	<script type="text/javascript">
	function preview(file) {
		var prevDiv = document.getElementById('preview');
		if(file.files && file.files[0]) {
			var reader = new FileReader();
			reader.onload = function(evt) {
				prevDiv.innerHTML = '<img src="' + evt.target.result + '"  onload="onPreviewLoad(this)" />';
			}
			reader.readAsDataURL(file.files[0]);
		}else{
			file.select();
			file.blur();
			var imgSrc = document.selection.createRange().text;
			prevDiv.innerHTML = '<div id="preDiv" class="img" style="filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale,src=\'' + imgSrc + '\'"></div><img id="preImg" style="filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=image,src=\''+imgSrc+'\');width:1px;visibility:hidden;overflow:hidden;" />';
			var objPreviewSizeFake = document.getElementById("preImg");
			var objPreviewFake = document.getElementById("preDiv");
			var reSizeTime = 0;
			function reSize() {
				reSizeTime++;
				setTimeout(function() {if(objPreviewSizeFake.offsetWidth != '1' || reSizeTime > 10) {autoSizePreview(objPreviewFake,objPreviewSizeFake.offsetWidth,objPreviewSizeFake.offsetHeight);}else{reSize();}},100);
			}
			reSize();
		}
	}

	function onPreviewLoad(sender) {
		autoSizePreview(sender,sender.offsetWidth,sender.offsetHeight);
	}

	function autoSizePreview(objPre,originalWidth,originalHeight) {
		var zoomParam = clacImgZoomParam(300,300,originalWidth,originalHeight);
		objPre.style.width = zoomParam.width + 'px';
		objPre.style.height = zoomParam.height + 'px';
		objPre.style.marginTop = zoomParam.top + 'px';
		objPre.style.marginLeft = zoomParam.left + 'px';
	}

	function clacImgZoomParam(maxWidth,maxHeight,width,height) {
		var param = {width:width,height:height,top:0,left:0};
		if(width>maxWidth || height>maxHeight) {
			rateWidth = width / maxWidth;
			rateHeight = height / maxHeight;
			if(rateWidth > rateHeight) {
				param.width = maxWidth;
				param.height = height / rateWidth;
			}else{
				param.width = width / rateHeight;
				param.height = maxHeight;
			}
		}
		param.left = (maxWidth - param.width) / 2;
		param.top = (maxHeight - param.height) / 2;
		return param;
	}
	</script>

(完)










