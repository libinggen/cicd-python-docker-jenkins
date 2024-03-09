# CICD-Python-Docker-Jenkins

```
ssh-keygen

SHA256:*** ***@kiyoshis-Air

cat ~/.ssh/id_rsa.pub

ssh-rsa 
***
***@kiyoshis-Air


GitHub -> current repository -> 'Settings' -> 'Security' -> 'Deploy Keys' -> Name the key -> Paste the key inside the 'Key' box -> tick the 'Allow Write Access' box -> click 'Add Key'

git remote add origin git@github.com:libinggen/pythonapp.git

git remote

ssh -T git@github.com

brew install jenkins-lts

brew services start jenkins-lts
brew services stop jenkins-lts
brew services restart jenkins-lts

linux:
sudo systemctl status jenkins.service

brew services list
brew services list | grep jenkins

localhost:8080

sudo cat /Users/zx/.jenkins/secrets/initialAdminPassword

Jenkins Dashboard > Manage Jenkins > Manage Plugins -> Docker Pipeline plugin -> Install -> restart Jenkins

/usr/local/opt/jenkins-lts/homebrew.mxcl.jenkins-lts.plist
/opt/homebrew/opt/jenkins-lts/homebrew.mxcl.jenkins-lts.plist

    <key>EnvironmentVariables</key>
    <dict>
      <key>PATH</key>
      <string>/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Applications/Docker.app/Contents/Resources/bin/:/Users/Kh0a/Library/Group\ Containers/group.com.docker/Applications/Docker.app/Contents/Resources/bin</string>
    </dict>

docker context use default
```
