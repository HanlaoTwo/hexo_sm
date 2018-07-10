---
title: Java运行Python
date: 2018-06-18 16:04:15
tags: note
---
```
import java.io.BufferedReader;
import java.io.InputStreamReader;

/**
 * Created by hello.
 */
public class testpy {

    private static String path = testpy.class.getResource("/").getPath() + "python/test.py";

    public static String hello() {
        String hello = ".....";
        try {
            System.out.println("start");
            System.out.println(path);
            Process pr = Runtime.getRuntime().exec("python " + path);
            BufferedReader in = new BufferedReader(new InputStreamReader(
                    pr.getInputStream()));
            String line;
            while ((line = in.readLine()) != null) {
                System.out.println(line);
                hello = line;
            }
            in.close();
            pr.waitFor();
            System.out.println("end");
        } catch (Exception e) {
            e.printStackTrace();
        }
        return hello;
    }
}
```