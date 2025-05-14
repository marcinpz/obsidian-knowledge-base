# Java Basics for DevOps

Essential Java concepts for DevOps tasks

## 1. Variables and Data Types
```java
// Primitive types
String serverName = "web01";     // String object
int port = 8080;                 // Integer
boolean isActive = true;         // Boolean
double cpuUsage = 75.5;          // Double

// Collections
String[] servers = {"web01", "web02"};              // Array
List<String> serverList = new ArrayList<>();        // ArrayList
Map<String, Integer> config = new HashMap<>();      // HashMap
```

## 2. Control Flow
```java
// If-else for service status
int statusCode = 200;
if (statusCode == 200) {
    System.out.println("Service is UP");
} else if (statusCode == 503) {
    System.out.println("Service Unavailable");
} else {
    System.out.println("Unknown status");
}

// For loop for server checks
String[] servers = {"web01", "web02", "web03"};
for (String server : servers) {
    System.out.println("Checking " + server);
}
```

## 3. Methods
```java
public class Monitor {
    // Method with parameter
    public String checkDiskSpace(int threshold) {
        int usage = 75;  // Simulated
        if (usage > threshold) {
            return "Warning: Disk usage at " + usage + "%";
        }
        return "Disk usage OK: " + usage + "%";
    }

    // Method with multiple parameters
    public String deployApp(String appName, String version, String env) {
        return "Deploying " + appName + " v" + version + " to " + env;
    }
}
```

## 4. File Operations
```java
import java.io.*;

// Reading config file
try (BufferedReader br = new BufferedReader(new FileReader("config.txt"))) {
    String configData = br.readLine();
}

// Writing log file
try (FileWriter fw = new FileWriter("deploy.log", true)) {
    fw.write("Deployment started\n");
}
```

## 5. Exception Handling
```java
try {
    // Attempt to connect to server
    connectToServer("web01");
} catch (IOException e) {
    System.out.println("Connection failed: " + e.getMessage());
} catch (Exception e) {
    System.out.println("Unexpected error: " + e.getMessage());
} finally {
    System.out.println("Cleanup complete");
}
```

## 6. Working with Classes
```java
import java.util.Date;

public class ServiceMonitor {
    private String serviceName;
    
    // Constructor
    public ServiceMonitor(String serviceName) {
        this.serviceName = serviceName;
    }
    
    // Method
    public String getStatus() {
        File pidFile = new File("/var/run/" + serviceName + ".pid");
        if (pidFile.exists()) {
            return serviceName + " is running";
        }
        return serviceName + " is not running";
    }
}

// Usage
ServiceMonitor monitor = new ServiceMonitor("nginx");
System.out.println(monitor.getStatus());
```

## 7. Simple DevOps Example
```java
import java.io.File;
import java.util.Date;

public class ServiceChecker {
    public static void main(String[] args) {
        String serviceName = "nginx";
        File pidFile = new File("/var/run/" + serviceName + ".pid");
        
        if (pidFile.exists()) {
            long uptime = new Date().getTime() - pidFile.lastModified();
            System.out.printf("%s is running (Uptime: %.2f hours)%n", 
                serviceName, uptime / 3600000.0);
        } else {
            System.out.println(serviceName + " is not running");
        }
    }
}
```

## DevOps-Relevant Tips
- Use `java.io` for file operations
- Use `java.util` for collections
- Implement proper exception handling
- Use meaningful class/method names
- Add JavaDoc comments for documentation
- Keep methods focused and concise

## Next Steps
- Learn about:
  - Maven/[[Gradle]] for builds
  - Java logging frameworks
  - Working with REST APIs
  - Java system utilities