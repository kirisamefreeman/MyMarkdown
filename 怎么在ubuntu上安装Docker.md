## 怎么在ubuntu上安装Docker
## 1.更新和安装依赖
```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release
```

## 2.设置 Docker 存储库 
```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## 3.下载Docker Desktop(deb包)
```
wget https://desktop.docker.com/linux/main/amd64/docker-desktop-4.19.0-amd64.deb?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64&_gl=1*1ttjjy2*_ga*MjUyOTg3OTMyLjE2ODUxOTUxMzE.*_ga_XJWPQMJYHQ*MTY4NTE5NTEzMS4xLjEuMTY4NTE5NTE0Ny40NC4wLjA.
```

## 4.更新软件包
```
sudo apt update
```


## 5.安装Docker Desktop
```
sudo apt install ./docker-desktop-4.19.0-amd64.deb
```

