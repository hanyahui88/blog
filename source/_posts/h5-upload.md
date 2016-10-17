---
title: H5 上传文件  
date: 2016-09-18 17:30:20
categories:  技术 
tags: [h5,上传文件]
---
使用ajax，对带文件的form表单提交（不用使用插件）<br/><!--more-->

    var formData = new FormData(document.getElementById("imgForm"));//获取form表单中的所有的数据，封装成formData
    $.ajax({
        url : 'http://localhost/global/upload',
        type : "POST",
        data :formData,
        async: false,
        cache: false,
        contentType: false,
        processData: false,
        success : function(data) {    
        },
        error : function(data) {  
        }
    });