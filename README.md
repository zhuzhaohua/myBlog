[教程请点这里](https://zhuzhaohua.com/technology/vue/20190915_myblog.html)


## 克隆至本地

## 安装依赖：
```
yarn 
```

## 注册并填写 评论组件所需要的key
参见[云淡风轻](https://ioliu.cn/2017/add-valine-comments-to-your-blog/)

在.vuepress/components/Valine.vue中修改appId和appKey
```
    new Valine({
      el: '#vcomments' ,
      appId: '',// your appId
      appKey: '', // your appKey
      notify:true, 
      verify:false, 
      avatar:'mm', 
      placeholder: 'just go go' 
    });
```

## 背景音乐
* .vuepress/public/mp3 中 放入喜欢的MP3文件(请支持正版！)
* 在.vuepress/components/Mp3Player.vue 中 修改文件路径


## 运行
```
npm run dev
```

## 编译
```
npm run build
```
