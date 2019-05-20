# liuyong
学习前端知识
<!DOCTYPE html>
<html lang="en">

<head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <style>
            * {
                  margin: 0;
                  padding: 0
            }

            html,
            body {
                  height: 100%
            }

            /* body{display: flex;justify-content: center;align-items: center} */
            .box {
                  width: 800px;
                  min-height: 200px;
                  border: 1px solid #a0a8f4;
                  border-radius: 10px;
                  margin: 50px auto;
                  padding-bottom: 10px
            }

            table {
                  border-spacing: 0;
                  border-collapse: collapse;
                  width: 97%;
                  margin-left: 10px;
                  text-align: center
            }

            tr,
            th {
                  height: 30px;
            }

            h3 {
                  background: #a0a8f4;
                  text-indent: 30px;
                  line-height: 30px;
                  height: 30px;
                  border-radius: 10px 10px 0 0;
                  color: #275d7d
            }

            .sousuobox {
                  height: 40px;
                  margin-top: 10px;
                  overflow: hidden
            }

            #sousuoinput {
                  float: left;
                  outline: none;
                  margin-left: 10px;
                  height: 28px;
            }

            .chaxun {
                  width: 50px;
                  height: 30px;
                  border-radius: 5px;
                  background: #2865a8;
                  float: left;
                  margin-left: 5px;
                  text-align: center;
                  cursor: pointer;
                  line-height: 30px
            }

            .creat {
                  width: 50px;
                  height: 30px;
                  border-radius: 5px;
                  background: #ce3c3e;
                  float: left;
                  margin-left: 5px;
                  text-align: center;
                  cursor: pointer;
                  line-height: 30px
            }

            table tr a:nth-of-type(1) {
                  display: inline-block;
                  background: #fa7070;
                  border-radius: 20%;
                  color: #fff
            }

            table tr a:nth-of-type(2) {
                  display: inline-block;
                  background: #53c3A6;
                  border-radius: 20%;
                  color: #fff
            }

            .bianjiboxwrap {
                  width: 300px;
                  width: 100%;
                  height: 100%;
                  background: rgba(100, 100, 100, 0.3);
                  position: absolute;
                  top: 0;
                  left: 0;
                  justify-content: center;
                  align-items: center;
                  display: none
            }

            .bianjibox {
                  width: 200px;
                  background: rgba(180, 180, 180, 1);
                  position: relative;
                  padding: 60px 40px
            }

            .bianjibox .quxiao {
                  width: 50px;
                  height: 30px;
                  border: 1px solid #333;
                  position: absolute;
                  bottom: 4%;
                  left: 20%;
                  cursor: pointer;
                  text-align: center;
            }

            .bianjibox .queding {
                  width: 50px;
                  height: 30px;
                  border: 1px solid #333;
                  position: absolute;
                  bottom: 4%;
                  right: 20%;
                  cursor: pointer;
                  text-align: center
            }

            span {
                  color: red;
                  font-size: 10px;
                  display: none
            }
      </style>
</head>

<body>
      <div class="box">

            <h3>学生信息管理</h3>
            <div class="sousuobox">
                  <input type="text" name="" id="sousuoinput">
                  <div class="chaxun">查询</div>
                  <div class="creat">新增</div>
            </div>
            <table border="1">
                  <tr>
                        <th>序号</th>
                        <th>姓名</th>
                        <th>手机号</th>
                        <th>QQ</th>
                        <th>专业</th>
                        <th>毕业时间</th>
                        <th>操作</th>
                  </tr>
            </table>
      </div>
      <div class="bianjiboxwrap">
            <div class="bianjibox">
                  <p>姓名<span>必须是2-5位中文</span></p>
                  <input type="text" name="" id="">
                  <p>手机号<span>手机号必须是11位纯数字</span></p>
                  <input type="text" name="" id="">
                  <p>QQ<span>QQ号必须是5-10位</span>></p>
                  <input type="text" name="" id="">
                  <p>专业<span>专业必须是中文至少两位</span></p>
                  <input type="text" name="" id="">
                  <p>毕业时间<span>请写入时间如：20190517</span></p>
                  <input type="text" name="" id="">
                  <div class="quxiao">取消</div>
                  <div class="queding">确定</div>
            </div>
      </div>

      <script src="http://libs.baidu.com/jquery/2.1.4/jquery.min.js"></script>
      <script>
            var table = document.querySelector('table')
            var chaxun = document.querySelector('.chaxun')
            var creat = document.querySelector('.creat')
            var ipt = document.querySelector('#sousuoinput')
            var storage = window.localStorage
            var bianjiboxwrap = document.querySelector('.bianjiboxwrap')
            var quxiao = document.querySelector('.quxiao')
            var queding = document.querySelector('.queding')
            let inputs = document.querySelectorAll('.bianjibox input')
            var spans=document.querySelectorAll('p span')
            var flag0 = false
            var flag1 = false
            var flag2 = false
            var flag3 = false
            var flag4 = false
            //页面加载完毕读取localstorage
            window.onload = function () {
                  // 设置storage.setItem('id',1)
                  //获取let id=storage.getItem('id')
                  //修改storage['id']=2
                  // 删除storage.removeItem('id')
                  let arr = JSON.parse(storage.getItem('info'))
                  console.log(arr)
                  for (let a = 0; a < arr.length; a++) {
                        table.innerHTML += `
                              <tr>
                                    <td>${arr[a].id}</td>
                                    <td>${arr[a].name}</td>
                                    <td>${arr[a].phone}</td>
                                    <td>${arr[a].qq}</td>
                                    <td>${arr[a].zhuanye}</td>
                                    <td>${arr[a].biyetime}</td>
                                    <td><a href="javascript:;" did="${arr[a].id}">删除</a> <a href="javascript:;" wid="${arr[a].id}">编辑</a></td>
                              </tr>
                        `
                  }

            }
            //增加信息
            creat.onclick = function () {
                  location.href = 'creat.html'
            }
            //查询信息
            chaxun.onclick = function () {
                  let arr=JSON.parse(storage.getItem('info'))
                  console.log(arr)
                  for(let c=0;c<arr.length;c++){
                        if(arr[c].name==ipt.value || arr[c].phone==ipt.value){
                              alert(`序号：${arr[c].id} 姓名：${arr[c].name} 手机号：${arr[c].phone} QQ：${arr[c].qq} 专业：${arr[c].zhuanye} 毕业时间：${arr[c].biyetime}`)
                        }
                  }
            }
            //删除和编辑，事件委托table
            table.onclick = function (eve) {
                  // console.log(eve.target)
                  if (eve.target.getAttribute('did')) {//删除按钮

                        if (confirm('您确定要删除吗')) {
                              let id = eve.target.getAttribute('did')
                              let oldarr = JSON.parse(storage.getItem('info'))
                              let newarr = []
                              for (let a = 0; a < oldarr.length; a++) {
                                    if (oldarr[a].id != id) {
                                          newarr.push(oldarr[a])
                                    }
                              }
                              storage.setItem('info', JSON.stringify(newarr))
                              eve.target.parentElement.parentElement.remove()
                        } else {

                        }
                  } else if (eve.target.getAttribute('wid')) {//编辑按钮
                        let tr = eve.target.parentElement.parentElement
                        let tds = tr.querySelectorAll('td')
                        bianjiboxwrap.style.display = 'flex'
                        console.log(inputs)
                        for (let a = 0; a < inputs.length; a++) {
                              inputs[a].value = tds[a + 1].innerHTML
                        }
                        quxiao.onclick = function () {//取消按钮
                              bianjiboxwrap.style.display = 'none'
                        }
                        queding.onclick = function () {//确定修改按钮
                              queding.onclick = function () {
                                    if (flag0 == true && flag1 == true && flag2 == true && flag3 == true && flag4 == true) {
                                          let obj = {}
                                          obj.id = tds[0].innerHTML
                                          obj.name = inputs[0].value
                                          obj.phone = inputs[1].value
                                          obj.qq = inputs[2].value
                                          obj.zhuanye = inputs[3].value
                                          obj.biyetime = inputs[4].value
                                          console.log(obj)
                                          let newarr = []
                                          let oldarr = JSON.parse(storage.getItem('info'))
                                          for (let b = 0; b < oldarr.length; b++) {
                                                if (oldarr[b].id != obj.id) {
                                                      newarr.push(oldarr[b])
                                                }
                                          }
                                          newarr.push(obj)
                                          storage.setItem('info', JSON.stringify(newarr))
                                          location.reload()
                                    } else {
                                          alert('请仔细检查格式')
                                    }
                              }
                        }
                  }
            }
            //修改输入框正则验证
            window.onkeyup = function () {
                   //姓名
                   reg=/^([\u4e00-\u9fa5]){2,5}$/
                  if(!reg.test(inputs[0].value)){
                        flag0=false
                        spans[0].style.display='inline'
                  }else{
                        flag0=true
                        spans[0].style.display='none'
                  }
                  //手机号
                  reg=/^1([38][0-9]|4[579]|5[0-3,5-9]|6[6]|7[0135678]|9[89])\d{8}$/
                  if(!reg.test(inputs[1].value)){
                        flag1=false
                        spans[1].style.display='inline'
                  }else{
                        flag1=true
                        spans[1].style.display='none'
                  }
                  //QQ
                  reg=/^[1-9]\d{4,9}$/
                  if(!reg.test(inputs[2].value)){
                        flag2=false
                        spans[2].style.display='inline'
                  }else{
                        flag2=true
                        spans[2].style.display='none'
                  }
                  //专业
                  reg=/^([\u4e00-\u9fa5]){2,10}$/
                  if(!reg.test(inputs[3].value)){
                        flag3=false
                        spans[3].style.display='inline'
                  }else{
                        flag3=true
                        spans[3].style.display='none'
                  }
                  //毕业时间
                  reg=/^[0-9]{8}$/
                  if(!reg.test(inputs[4].value)){
                        flag4=false
                        spans[4].style.display='inline'
                  }else{
                        flag4=true
                        spans[4].style.display='none'
                  }
            }
      </script>
</body>

</html>
