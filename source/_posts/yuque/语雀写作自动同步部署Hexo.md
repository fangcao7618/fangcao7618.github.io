
---

title: 语雀写作自动同步部署Hexo

date: 2019-06-20 10:40:08 +0800

tags: []

---
语雀和Hexo之前都有单独使用过，都很舒服，今天偶然看到一篇大佬的文章，居然可以把这两个结合起来使用，这岂不是美滋滋，爽歪歪，所以说心动不如行动，搞起来~~~<br />在实施的过程中，由于自己太菜，有好多坑，搞了好长时间才搞好，不容易，写这样一个文章记录一下<br />[]()<br />[]()
<a name="DjNfG"></a>
# [](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#%E4%B8%80%E3%80%81%E6%89%80%E9%9C%80%E7%8E%AF%E5%A2%83)一、所需环境
[]()
<a name="wISsi"></a>
## [](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#1-%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F)1.操作系统
最好Linux，若在Windows中就装一下虚拟机<br />[]()
<a name="SLSJg"></a>
## [](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#2-%E6%89%80%E9%9C%80%E7%8E%AF%E5%A2%83%E8%BD%AF%E4%BB%B6)2.所需环境软件

1. Git
1. Node.Js
1. Hexo
1. Ruby<br />[]()[](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#%E4%BA%8C%E3%80%81%E5%AE%9E%E7%8E%B0%E6%AD%A5%E9%AA%A4)二、实现步骤<br />利用**Hexo+Github+Triavs-ci**来实现在语雀上面写着之后自动部署到Hexo上面去，这么做只能用舒服来形容，嘻嘻！<br />[]()[](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#1-%E4%BB%8B%E7%BB%8D)1.介绍<br />[]()[](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#1%EF%BC%89Hexo)1）[Hexo](https://hexo.io/zh-cn/)<br />要怎么来部署就不要我在这多说什么了，我的博客有这样的教程，附上我的[博客地址](https://selfishluck.top/)。<br />[]()[](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#2%EF%BC%89Github)2）[Github](https://github.com/)<br />作为一个程序猿必备，略过，没有的，嗯哼，可以不用看了。<br />[]()[](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#3%EF%BC%89Triavs-ci)3）[Triavs-ci](https://travis-ci.org/)<br />开源持续集成构建项目，它与jenkins有点像，可以直接用你的Github账号登录，同步你的仓库，很是方便，页面也比较简洁好看。<br />[]()[](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#4%EF%BC%89yuque-hexo)4）[yuque-hexo](https://github.com/x-cold/yuque-hexo)<br />一个Hexo的插件，看名字就知道用来干什么的了，所以你猜的没有错，他就是用来同步语雀到Hexo的插件，这是开源插件，附上开源库[地址](https://github.com/x-cold/yuque-hexo)。感谢大佬的插件。<br />使用起来也很简单就只需要安装好在package.json配置一下就好了。<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318031853-7d893029-fa9f-4b9a-af0a-8ba2b231e1af.png#align=left&display=inline&height=186&name=image.png&originHeight=233&originWidth=669&size=22559&status=done&width=535#align=left&display=inline&height=233&originHeight=233&originWidth=669&status=done&width=669)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318031853-7d893029-fa9f-4b9a-af0a-8ba2b231e1af.png#align=left&display=inline&height=186&name=image.png&originHeight=233&originWidth=669&size=22559&status=done&width=535)<br />还在配置一下命令，不然编译生成的时候不会同步语雀的文章，也在package.json文件中配置<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318156049-3bab5286-79df-4217-88c9-2796b604d986.png#align=left&display=inline&height=126&name=image.png&originHeight=157&originWidth=648&size=16435&status=done&width=518#align=left&display=inline&height=157&originHeight=157&originWidth=648&status=done&width=648)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318156049-3bab5286-79df-4217-88c9-2796b604d986.png#align=left&display=inline&height=126&name=image.png&originHeight=157&originWidth=648&size=16435&status=done&width=518)<br />**具体可以参考我的**[**package.json**](https://github.com/iqiuzixuan/Source-Hexo/blob/master/package.json)**文件**<br />[]()[](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#2-%E6%93%8D%E4%BD%9C%E6%B5%81%E7%A8%8B)2.操作流程<br />[]()[](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#1%EF%BC%89%E9%85%8D%E7%BD%AEHexo)1）配置Hexo<br />**这里简单说一下要注意的地方，具体教程网上有很多。**
- 增加`hexo-deployer-git`依赖，防止部署时报错。
| copynpm install --save hexo-deployer-git |
| :--- |

- 增加`hexo-util`到`dev`依赖，防止travis的npm版本<3,出现的`Error: Cannot find module 'hexo-util'`错误。<br />
| copynpm install --save-dev hexo-util |
| :--- |

[]()
<a name="imfQC"></a>
### [](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#2%EF%BC%89%E9%85%8D%E7%BD%AEGithub)2）配置Github

- 在Github上面建两个库（也不一定要两个，也可以利用两个代码分支来进行，我这里用两个仓库做栗子）

一个仓库拥来存放Hexo编译前的代码库。另一个用来存放编译后用来开启Pages的仓库。<br />在本地创建好的Hexo可以提交到源码的仓库了。可以也把Pages的也配置好。<br />[]()
<a name="HLoO7"></a>
### [](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#3%EF%BC%89%E9%85%8D%E7%BD%AETravis-CI)3）配置Travis CI

- **第一步**我们需要有一个 Travis-CI 的账号，直接进入[Travis-CI](https://travis-ci.org/)官网，用自己的Github账号授权登录即可。

然后可以看到当前账号的所有代码仓库，接下来将博客项目的状态设置为启用。<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552314341771-2e107342-97c3-4300-9e60-51b0cce1346a.png#align=left&display=inline&height=367&name=image.png&originHeight=459&originWidth=949&size=37799&status=done&width=759#align=left&display=inline&height=459&originHeight=459&originWidth=949&status=done&width=949)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552314341771-2e107342-97c3-4300-9e60-51b0cce1346a.png#align=left&display=inline&height=367&name=image.png&originHeight=459&originWidth=949&size=37799&status=done&width=759)

- **第二步**创建一个部署在 Travis CI 上面的 SSH key 利用这个 SSH key 可以让 Travis CI 向我们自己的项目提交代码(也就是将博客部署到Page)。这如果你在之前部署Hexo的时候已经创建过了，就可以直接用那个公钥来添加到Github里面去，添加好之后大概就是图片上的样子。

**这里提一下，有的时候你的本地向GitHub提交提交不上去，但之前还是可以的，这时候可以检查GitHub的SSH密钥这里，可能是因为安全问题，官方给你暂时冻结了这个密钥，冻结的情况下这里的Delete旁边就会多一个激活按钮，点一下就好了。**<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552314698412-8580e7f0-1267-4708-b219-449e15e364d9.png#align=left&display=inline&height=561&name=image.png&originHeight=701&originWidth=1411&size=79239&status=done&width=1129#align=left&display=inline&height=701&originHeight=701&originWidth=1411&status=done&width=1411)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552314698412-8580e7f0-1267-4708-b219-449e15e364d9.png#align=left&display=inline&height=561&name=image.png&originHeight=701&originWidth=1411&size=79239&status=done&width=1129)

- **第三步加密私钥**

**加密密钥的时候一定要在Linux操作系统下进行，不然travis-ci之后进行解密的时候会报错，目前官方就是这样的一个BUG，暂时无解。**<br />**Windows的同学可以在Linux虚拟机中把你的Hexo源码仓库clone进行下面的操作。**

- **这里还需要Ruby来支撑，所以还需安装Ruby，有几种方式，个人推荐还是老老实实编译安装最好**
  - 下载ruby

下载最新版的 Ruby 压缩文件。[请点击这里下载](http://www.ruby-lang.org/en/downloads/)。也可以使用wget命令<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552316340445-c6243017-c640-47d6-875e-32c36a3199ac.png#align=left&display=inline&height=47&name=image.png&originHeight=59&originWidth=716&size=8803&status=done&width=573#align=left&display=inline&height=59&originHeight=59&originWidth=716&status=done&width=716)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552316340445-c6243017-c640-47d6-875e-32c36a3199ac.png#align=left&display=inline&height=47&name=image.png&originHeight=59&originWidth=716&size=8803&status=done&width=573)
```
- 下载 Ruby 之后，解压到新创建的目录下：
```

```bash
$ tar -xvzf ruby-2.2.3.tgz    
$ cd ruby-2.2.3
```

```
- 现在，配置并编译源代码，如下所示：
```

```bash
$ ./configure
$ make
$ sudo make install
```
装后，通过在命令行中输入以下命令来确保一切工作正常：
```bash
$ruby -v

ruby 2.2.3……
```

如果一切工作正常，将会输出所安装的 Ruby 解释器的版本，如上所示。如果您安装了其他版本，则会显示其他不同的版本。

- **安装travis（如果在国内的网络环境下建议安装之前先[换源](https://gems.ruby-china.com/))**
> $ gem install travis

- 那么之前把公钥文件配置好了，然后现在就要配置私钥文件，在 hexo 项目下面建立一个 `.travis` 的文件夹来放置需要配置的文件和travis的配置文件travis.yml。Windows和Linux下无法创建和创建报错可以用命令`mkdir ./.travis`进行创建文件夹，用命令`touch ./.travis.yml`来创建travis的配置文件。切换到.travis文件夹下
```javascript
![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552316024043-dfd7b632-8a75-4634-ad76-4cb77158b415.png#align=left&display=inline&height=46&name=image.png&originHeight=57&originWidth=721&size=17007&status=done&width=577)<br />用命令行工具登录：
```
> travis login --auto

这时候会让你输入你的Github账号（邮箱）和密码，也可以使用GitHub的Token来进行登录
> travis login --github-token 具体的Token --auto

- 然后将私钥 `id_rsa` 复制到 `.travis` 文件夹，用命令行工具进行加密：
> $ travis encrypt-file id_rsa --add

这时候在之前创建好的.travis.yml文件里面就会被写入一些密钥的信息，大概如此：<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552317097064-e2ec9597-d562-491e-88e5-e4c6f928d651.png#align=left&display=inline&height=245&name=image.png&originHeight=307&originWidth=893&size=24988&status=done&width=714#align=left&display=inline&height=307&originHeight=307&originWidth=893&status=done&width=893)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552317097064-e2ec9597-d562-491e-88e5-e4c6f928d651.png#align=left&display=inline&height=245&name=image.png&originHeight=307&originWidth=893&size=24988&status=done&width=714)<br />在你的Travis的项目设置中也会出现密钥<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552317190879-6334a8f8-c53c-48d9-b06f-92a387a6e315.png#align=left&display=inline&height=212&name=image.png&originHeight=265&originWidth=2140&size=31214&status=done&width=1712#align=left&display=inline&height=265&originHeight=265&originWidth=2140&status=done&width=2140)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552317190879-6334a8f8-c53c-48d9-b06f-92a387a6e315.png#align=left&display=inline&height=212&name=image.png&originHeight=265&originWidth=2140&size=31214&status=done&width=1712)

- 接下来就要配置 `.travis.yml`

首先我们要改一下生成的解密信息，因为这个里面的in和out的文件位置是相对于本地环境来生成的，如果在Travis上面跑的时候位置会发生变化这样运行的时候就会报错，改完之后大概这样子：<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552317499260-cb565ce2-c8ef-4a6f-a871-c97c50c808e0.png#align=left&display=inline&height=58&name=image.png&originHeight=72&originWidth=904&size=9605&status=done&width=723#align=left&display=inline&height=72&originHeight=72&originWidth=904&status=done&width=904)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552317499260-cb565ce2-c8ef-4a6f-a871-c97c50c808e0.png#align=left&display=inline&height=58&name=image.png&originHeight=72&originWidth=904&size=9605&status=done&width=723)

- 为了让 git 默认连接 SSH 还要创建一个 `ssh_config` 文件。在 `.travis` 文件夹下创建一个 `ssh_config` 文件，输入以下内容：
> Host github.com
>     User git
>     StrictHostKeyChecking no
>     IdentityFile ~/.ssh/id_rsa
>     IdentitiesOnly yes

这样，当向项目 push 代码的时候 travis CI 就会根据 `.travis.yml` 的内容去部署我们的项目了。<br />**具体可以参考我的**[**.travis.yml**](https://github.com/iqiuzixuan/Source-Hexo/blob/master/.travis.yml)**文件**<br />**这里要提一下，我们在向Hexo源码仓库Push的时候不要提交本地编译生成的node_modules文件夹，不然到时候在上面跑的时候会有权限问题，npm会根据package.json上面的信息自己下模块的，所以不用当选，具体的涉及到npm的运行原理这里不提了，想了解的可以自行百度哈。**<br />**<br />[]()
<a name="9RIcT"></a>
### [](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#4%EF%BC%89%E9%85%8D%E7%BD%AEServerless%E6%9C%8D%E5%8A%A1)4）配置Serverless服务
目前阿里云和腾讯云都有serverless服务，免费的额度完全够用了，下面介绍一下腾讯云如何配置

- 创建函数

[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318260256-3e99c270-068c-4d0a-acdf-2c7cbb2a51ac.png#align=left&display=inline&height=773&name=image.png&originHeight=966&originWidth=1655&size=135221&status=done&width=1324#align=left&display=inline&height=966&originHeight=966&originWidth=1655&status=done&width=1655)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318260256-3e99c270-068c-4d0a-acdf-2c7cbb2a51ac.png#align=left&display=inline&height=773&name=image.png&originHeight=966&originWidth=1655&size=135221&status=done&width=1324)

- serverless 函数配置

点击完成即可，之后在配置具体函数代码<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318381439-b01e377f-2a66-4989-b365-08b8a0bd07a2.png#align=left&display=inline&height=659&name=image.png&originHeight=1066&originWidth=1207&size=91516&status=done&width=746#align=left&display=inline&height=1066&originHeight=1066&originWidth=1207&status=done&width=1207)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318381439-b01e377f-2a66-4989-b365-08b8a0bd07a2.png#align=left&display=inline&height=659&name=image.png&originHeight=1066&originWidth=1207&size=91516&status=done&width=746)<br />示例：

```javascript
<?php
function main_handler($event, $context) {
    // 解析语雀post的数据
    $update_title = '';
    if($event->body){
        $yuque_data= json_decode($event->body);
        $update_title .= $yuque_data->data->title;
    }
    // default params
    $repos = '';  // 你的仓库id 或 slug
    $token = ''; // 你travis-cide的登录token
    $message = date("Y/m/d").':更新啦:'.$update_title; // 你这里是更新信息可自定义
    $branch = 'master'; // 你GitHub分支
    // post params
    $queryString = $event->queryString;
    $q_token = $queryString->token ? $queryString->token : $token;
    $q_repos = $queryString->repos ? $queryString->repos : $repos;
    $q_message = $queryString->message ? $queryString->message : $message;
    $q_branch = $queryString->branch ? $queryString->branch : 'master';
    echo($q_token);
    echo('===');
    echo ($q_repos);
    echo ('===');
    echo ($q_message);
    echo ('===');
    echo ($q_branch);
    echo ('===');
    //request travis ci
    $res_info = triggerTravisCI($q_repos, $q_token, $q_message, $q_branch);

    $res_code = 0;
    $res_message = '未知';
    if($res_info['http_code']){
        $res_code = $res_info['http_code'];
        switch($res_info['http_code']){
            case 200:
            case 202:
                $res_message = 'success';
            break;
            default:
                $res_message = 'faild';
            break;
        }
    }
    $res = array(
        'status'=>$res_code,
        'message'=>$res_message
    );
    return $res;
}

/*
* @description  travis api , trigger a build
* @param $repos string 仓库ID、slug
* @param $token string 登录验证token
* @param $message string 触发信息
* @param $branch string 分支
* @return $info array 回包信息
*/
function triggerTravisCI ($repos, $token, $message='yuque update', $branch='master') {
    //初始化
    $curl = curl_init();
    //设置抓取的url
    curl_setopt($curl, CURLOPT_URL, 'https://api.travis-ci.org/repo/'.$repos.'/requests');
    //设置获取的信息以文件流的形式返回，而不是直接输出。
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
    //设置post方式提交
    curl_setopt($curl, CURLOPT_CUSTOMREQUEST, "POST");
    //设置post数据
    $post_data = json_encode(array(
        "request"=> array(
            "message"=>$message,
            "branch"=>$branch
        )
    ));
    $header = array(
      'Content-Type: application/json',
      'Travis-API-Version: 3',
      'Authorization:token '.$token,
      'Content-Length:' . strlen($post_data)
    );
    curl_setopt($curl, CURLOPT_HTTPHEADER, $header);
    curl_setopt($curl, CURLOPT_POSTFIELDS, $post_data);
    //执行命令
    $data = curl_exec($curl);
    $info = curl_getinfo($curl);
    //关闭URL请求
    curl_close($curl);
    return $info;
}
?>
```


- 这里有几个需要获取的参数：
  - travis登录token，在travis-ci.org 中设置界面获取：

[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318615826-585c7915-10c0-4540-9c78-c430cbef71a7.png#align=left&display=inline&height=347&name=image.png&originHeight=434&originWidth=1576&size=60737&status=done&width=1261#align=left&display=inline&height=434&originHeight=434&originWidth=1576&status=done&width=1576)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318615826-585c7915-10c0-4540-9c78-c430cbef71a7.png#align=left&display=inline&height=347&name=image.png&originHeight=434&originWidth=1576&size=60737&status=done&width=1261)
```
- 仓库ID 或 扩展名
```
使用findder 或者 postman 发起一个请求：
> https://api.travis-ci.org/owner/github用户名/repos


[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318860737-c1e8c256-106b-45bc-90ed-19054fa6629d.png#align=left&display=inline&height=811&name=image.png&originHeight=1014&originWidth=2149&size=159364&status=done&width=1719#align=left&display=inline&height=1014&originHeight=1014&originWidth=2149&status=done&width=2149)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318860737-c1e8c256-106b-45bc-90ed-19054fa6629d.png#align=left&display=inline&height=811&name=image.png&originHeight=1014&originWidth=2149&size=159364&status=done&width=1719)

- 配置触发方式

一般会得到这么个api：<br />[https://service-8x9gl1u7-1258196125.ap-shanghai.apigateway.myqcloud.com/release/yuque-hexo](https://service-8x9gl1u7-1258196125.ap-shanghai.apigateway.myqcloud.com/release/yuque-hexo)<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318938197-0541ac93-4523-44cf-9c9a-4c0459151958.png#align=left&display=inline&height=356&name=image.png&originHeight=445&originWidth=1251&size=31093&status=done&width=1001#align=left&display=inline&height=445&originHeight=445&originWidth=1251&status=done&width=1251)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552318938197-0541ac93-4523-44cf-9c9a-4c0459151958.png#align=left&display=inline&height=356&name=image.png&originHeight=445&originWidth=1251&size=31093&status=done&width=1001)<br />[]()
<a name="sSsbX"></a>
### [](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#5%EF%BC%89%E9%85%8D%E7%BD%AE%E8%AF%AD%E9%9B%80)5）配置语雀
配置一个仓库（公开的仓库）的webhook:<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552319100028-0aa382b9-94dc-492e-9e1e-8e68651af93e.png#align=left&display=inline&height=466&name=image.png&originHeight=583&originWidth=1301&size=62732&status=done&width=1041#align=left&display=inline&height=583&originHeight=583&originWidth=1301&status=done&width=1301)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552319100028-0aa382b9-94dc-492e-9e1e-8e68651af93e.png#align=left&display=inline&height=466&name=image.png&originHeight=583&originWidth=1301&size=62732&status=done&width=1041)<br />可以选择所有更新触发或者主动触发，主动触发的意思即发布需要勾选一个选项才会触发webhook。具体可参见[语雀文档](https://www.yuque.com/yuque/developer/doc-webhook)；<br />将serverless生成的api填入,可以在链接后面带参数：

```javascript
token 登录token
repos 仓库id
message 提交信息
branch 分支

示例：
https://service-8x9gl1u7-1258196125.ap-shanghai.apigateway.myqcloud.com/release/yuque-hexo?repos=xxx&token=xxx&message=xxx&branch=xxx
```

如果不在链接带参数则写在serverless函数内。<br />[]()
<a name="LALv6"></a>
### [](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#6%EF%BC%89%E5%A4%A7%E5%8A%9F%E5%91%8A%E6%88%90)6）大功告成
发布或者更新一篇文章后，我们前往travis-ci,可以看到已经触发了一次构建请求：<br />[![image.png](https://cdn.nlark.com/yuque/0/2019/png/240833/1552319240278-88c72888-1646-41d4-8f5a-549035b99065.png#align=left&display=inline&height=302&name=image.png&originHeight=377&originWidth=1980&size=71788&status=done&width=1584#align=left&display=inline&height=377&originHeight=377&originWidth=1980&status=done&width=1980)](https://cdn.nlark.com/yuque/0/2019/png/240833/1552319240278-88c72888-1646-41d4-8f5a-549035b99065.png#align=left&display=inline&height=302&name=image.png&originHeight=377&originWidth=1980&size=71788&status=done&width=1584)<br />构建完成后，咱们的博客上已经妥妥的展示出来拉~<br />[]()
<a name="GYZwR"></a>
# [](https://selfishluck.top/2019/03/10/yuque/%E8%AF%AD%E9%9B%80%E5%86%99%E4%BD%9C%E8%87%AA%E5%8A%A8%E5%90%8C%E6%AD%A5%E9%83%A8%E7%BD%B2Hexo/#%E5%8F%82%E8%80%83%E8%B5%84%E6%96%99)参考资料
[Nero](https://www.yuque.com/u46795/blog/dlloc7#8072e205)的语雀<br />
<br />转自：[https://sunnybob.github.io/2019/01/11/%E8%AF%AD%E9%9B%80%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2hexo+GithubPages%E5%8D%9A%E5%AE%A2/](https://sunnybob.github.io/2019/01/11/%E8%AF%AD%E9%9B%80%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2hexo+GithubPages%E5%8D%9A%E5%AE%A2/)

