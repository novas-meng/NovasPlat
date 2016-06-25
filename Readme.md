简介：提供并行化机器学习算法的简单调用。
使用，首先确保正确安装好hadoop，本系统使用hadoop 1.2.1版本。jdk 1.7版本。

1：在etc/profile 中导入环境变量 NOVAS_HOME
export NOVAS_HOME=/usr/Novas
之后，保存，注销用户，让环境变量生效。
2：更改文件夹所属用户  sudo chown -hR novas /usr/Novas
其中，novas为用户名。/usr/Novas为项目根目录。
3:运行 ./{$NOVAS_HOME}/bin/dameon.
启动服务

客户端调用过程 需要使用novas包进行调用。详情见https://github.com/novas-meng/novas

调用实例
       AlgoProxy algoProxy=new AlgoProxy("192.168.1.150",9087,9081);
        HashMap<String,Class> params=algoProxy.getMethod("fcm").getParamsToType();
        for(Map.Entry<String,Class> entry:params.entrySet())
        {
            System.out.println(entry.getKey());
            System.out.println(entry.getValue().getName());
        }
        //以下为具体调用方法
        //1:设置参数
        HashMap<String,Object> hashMap=new HashMap<>();
        hashMap.put("m",3);
        hashMap.put("c",2);
        hashMap.put("inputPath","/home/novas/data");
        hashMap.put("outputPath","/home/novas/martix");
        //2：获取方法MethodProxy对象
        MethodProxy proxy=algoProxy.getMethod("fcm");
        //3:将参数赋值给MethodProxy
        try {
            proxy.setParamsToValue(hashMap);
            //4:调用方法
            algoProxy.callMethod(proxy);
        } catch (ParamsNameException e) {
            e.printStackTrace();
        } catch (ParamsTypeException e) {
            e.printStackTrace();
        }

