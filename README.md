# RtmpPush
简单的直播推流


流媒体服务器有诸多选择，如商业版的Wowza。但我选择的是免费的Nginx（nginx-rtmp-module）。Nginx本身是一个非常出色的HTTP服务器，它通过nginx的模块nginx-rtmp-module可以搭建一个功能相对比较完善的流媒体服务器。这个流媒体服务器可以支持RTMP和HLS。 Nginx配合SDK做流媒体服务器的原理是: Nginx通过rtmp模块提供rtmp服务, SDK推送一个rtmp流到Nginx, 然后客户端通过访问Nginx来收看实时视频流。 HLS也是差不多的原理,只是最终客户端是通过HTTP协议来访问的,但是SDK推送流仍然是rtmp的。 下面是一款已经集成rtmp模块的windows版本的Nginx。下载后，即可直接使用 下载链接：https://github.com/illuspas/nginx-rtmp-win32

1、rtmp端口配置 配置文件在/conf/nginx.conf RTMP监听 1935 端口，启用live 和hls 两个application 这里写图片描述 所以你的流媒体服务器url可以写成：rtmp://（服务器IP地址）:1935/live/xxx 或 rtmp://（服务器IP地址）:1935/hls/xxx 例如我们上面写的 rtmp://192.168.1.104:1935/live/12345

HTTP监听 8080 端口，

:8080/stat 查看stream状态 :8080/index.html 为一个直播播放与直播发布测试器 :8080/vod.html 为一个支持RTMP和HLS点播的测试器 2、启动nginx服务 双击nginx.exe文件或者在dos窗口下运行nginx.exe，即可启动nginx服务： 这里写图片描述

1）启动任务管理器，可以看到nginx.exe进程 这里写图片描述

2）打开网页输入http://localhot:8080,出现如下画面： 这里写图片描述 显示以上界面说明启动成功。

第三部分：直播流的播放

主播界面： 这里写图片描述

上面说过了只要支持RTMP流传输协议的播放器都可以收看到我们的直播。下面举两个例子吧： （1）window端播放器VLC 这里写图片描述

这里写图片描述

（2）android端播放器ijkplayer ijkplayer的使用请参考Android ijkplayer的使用解析

private void initPlayer() {
    player = new PlayerManager(this);
    player.setFullScreenOnly(true);
    player.setScaleType(PlayerManager.SCALETYPE_FILLPARENT);
    player.playInFullScreen(true);
    player.setPlayerStateListener(this);
    player.play("rtmp://192.168.1.104:1935/live/12345");
}
1 2 3 4 5 6 7 8 这里写图片描述
