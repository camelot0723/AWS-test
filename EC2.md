# EC2

## 1.AWS Management Console創建EC2
![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548575979695_Snipaste_2019-01-27_15-54-33.png)

## 2.點選Launch Instance
![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548576201124_Snipaste_2019-01-27_16-00-40.png)

## 3.選擇AMI

(1)先點選左方Community AMIs
(2) 在上方欄位輸入: 1a15c
(3) 出現ami-1a15c77b
(4) 點選Select

![](https://d2mxuefqeaa7sj.cloudfront.net/s_55D1D6958FBD50318889E6D97A28D06E26D37985CA8124C172AE8457DB77162F_1548743584211_21.jpg)

## 4.選擇Instance Type

(1)先點選t2.micro
(2)再按右下角的Next:Configure Instance Details

![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548580208832_Snipaste_2019-01-27_16-17-35.png)

## 5.Configure Instance

 (1)Network: 選擇先前創建好的cc104_web_vpc
 (2)Subent: 選擇先前創建好的cc104_web_subnet
 (3)IAM role選擇先前創建好的cc104_ec2_role

![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548583828905_Snipaste_2019-01-27_17-01-45.png)


(4)Advanced Details-User data

- 輸入下方內容設定User data
- 點選Next: Add Storage
![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548580708221_Snipaste_2019-01-27_17-16-24.png)

    #!/bin/bash 
    yum update -y 
    yum install -y docker git awscli ruby 
    usermod -a -G docker ec2-user 
    service docker start 
    chkconfig docker on 
    $(aws ecr get-login --no-include-email --region ap-northeast-1) 
    docker pull 204065533127.dkr.ecr.ap-northeast-1.apmazonaws.com/cc104devops-repo:0.0.1 
    docker run -p 80:5000 -d --name cc104-devops 204065533127.dkr.ecr.ap-northeast-1.amazonaws.com/cc104devops-repo:0.0.1 
    
    sudo curl -O https://aws-codedeploy-ap-northeast-1.s3.amazonaws.com/latest/install 
    sudo chmod +x ./install 
    sudo ./install auto


## 6.Add Storage

(1) 使用預設值即可
(2)設定好後，點選Next: Add Tags

![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548580934010_Snipaste_2019-01-27_17-22-08.png)

## 7.Add Tags

(1) 可自行設定需要的標籤(但第一行Key的部分要打Name)
(2) 設定好後，點選右下角Next: Configure Security Group

![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548583994742_Snipaste_2019-01-27_17-28-10.png)

## 8.Configure Security Group

(1) Select an existing security group(選擇創建VPC時，預設會自動創建的防火牆)
(2) 點選右下角 Review and Launch

![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548585651584_Snipaste_2019-01-27_18-40-28.png)

## 9.確認內容無誤後，點選Launch
![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548585856241_Snipaste_2019-01-27_18-42-30.png)

![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548585861017_Snipaste_2019-01-27_18-43-18.png)

![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548585909766_Snipaste_2019-01-27_18-43-49.png)

## 10.Select a key pair  

(1)選擇之前已創建的key pair(cc104key)
(2)設定完成後，點選Launch instances

![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548586004371_Snipaste_2019-01-27_18-46-15.png)

## 11.EC2創建完成後的頁面
- 點選右下角View Instances
![](https://d2mxuefqeaa7sj.cloudfront.net/s_44766B39D1BE4B8BB1DC5E3A308DF38A07E9CA4C84846794E82C5BEE00E3DAC3_1548586166385_Snipaste_2019-01-27_18-49-18.png)

## 

