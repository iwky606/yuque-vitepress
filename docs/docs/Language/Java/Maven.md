## 常用setting.xml配置
`~/.m/settings.xml`

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" 
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 
  http://maven.apache.org/xsd/settings-1.0.0.xsd">

  <mirrors>
    <mirror>
      <id>central-mirror</id>

      <mirrorOf>central</mirrorOf>

      <url>https://maven.aliyun.com/repository/public</url>

    </mirror>

  </mirrors>

  <profiles>
    <profile>
      <id>default</id>

      <repositories>
        <repository>
          <id>central</id>

          <url>https://repo.maven.apache.org/maven2</url>

          <releases>
            <enabled>true</enabled>

          </releases>

          <snapshots>
            <enabled>true</enabled>

          </snapshots>

        </repository>

      </repositories>

    </profile>

  </profiles>

  <activeProfiles>
    <activeProfile>default</activeProfile>

  </activeProfiles>


</settings>

```





## maven本地打包
```bash
mvn install:install-file -Dfile=/code/project1/target/dingding-2.0.5.jar -DgroupId=com.oneq.cc -DartifactId=dingding-util -Dversion=1.0 -Dpackaging=jar
```

