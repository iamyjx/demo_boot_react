# demo_boot_react


## 前后端统一用maven管理，前端部署采用frontend-maven-plugin，maven-antrun-plugin整合至后端一键部署
```
  <plugin>
                  <groupId>com.github.eirslett</groupId>
                  <artifactId>frontend-maven-plugin</artifactId>
                  <version>1.6</version>
                  <configuration>
                      <workingDirectory>./</workingDirectory>
                      <installDirectory>target</installDirectory>
                  </configuration>
                  <executions>
                      <execution>
                          <id>install node and npm</id>
                          <goals>
                              <goal>install-node-and-npm</goal>
                          </goals>
                          <configuration>
                              <nodeVersion>v10.16.0</nodeVersion>
                              <npmVersion>6.9.0</npmVersion>
                          </configuration>
                      </execution>
                      <execution>
                          <id>npm install</id>
                          <goals>
                              <goal>npm</goal>
                          </goals>
                          <configuration>
                              <arguments>install</arguments>
                          </configuration>
                      </execution>
                      <execution>
                          <id>npm run build</id>
                          <goals>
                              <goal>npm</goal>
                          </goals>
                          <configuration>
                              <arguments>run build</arguments>
                          </configuration>
                      </execution>
                  </executions>
              </plugin>
  
              <plugin>
                  <artifactId>maven-antrun-plugin</artifactId>
                  <executions>
                      <execution>
                          <phase>generate-resources</phase>
                          <configuration>
                              <target>
                                  <!-- 打印信息 -->
                                  <echo message="删除复制前端编译文件" />
                                  <!-- 删除文件夹 -->
                                  <delete dir="../backend/src/main/resources/public" />
                                  <copy todir="../backend/src/main/resources/public">
                                      <fileset dir="${project.basedir}/build"/>
                                  </copy>
                                  <copy tofile="../backend/src/main/resources/templates/index.html" file="${project.basedir}/build/index.html" overwrite="true">
                                  </copy>
                              </target>
                          </configuration>
                          <goals>
                              <goal>run</goal>
                          </goals>
                      </execution>
                  </executions>
              </plugin>
```

## 前后端可分别进行开发
    开发调试，package.json将非text/html的api请求代理至后端
    在package.json中添加"proxy": "http://localhost:8080"
      





