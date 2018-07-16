# java IO

标签： java 实习

----

1. java io 的开始：文件
   
 流的本质也是对文件的处理

java 文件处理示例：

```
package com.test;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.PrintWriter;
import java.io.Reader;
import java.net.URL;
import java.net.URLConnection;

public class TestIO {

	public static void main(String[] args) throws IOException {
		
		String src = "https://img3.doubanio.com/icon/u1001945-45.jpg";
		URL url = new URL(src);
		URLConnection uc =url.openConnection();
//		uc.getInputStream()
		
		String pathname = "d:" + File.separator 
				+ "abc" + File.separator 
				+ "123.txt";
		File inputFile = new File(pathname);
//file.separator 是处于跨平台性和健壮性考虑的
//  在linux下编译 / ，在win下编译为\\
		
		//其他方法二
//		inputFile = new File("d:" + File.separator + "abc", "123.txt");
        //其他方法三
//		File parentDir = new File("d:" + File.separator + "abc");
//		inputFile = new File(parentDir, "123.txt");
		
		InputStream fis = new FileInputStream(inputFile);
		fis = uc.getInputStream();
	//因为用字节流来读媒介，所以对应inputstream
   //因为媒介对象是文件，所以用到子类fileinputstream
   
	
		String pathnameOutput = "e:" + File.separator 
				+ "xyz" + File.separator
				+ "456.txt";
		File outputFile = new File(pathnameOutput);
		if (!outputFile.getParentFile().exists())
			outputFile.getParentFile().mkdirs();
		OutputStream fos = new FileOutputStream(outputFile);
		
		byte[] buffer = new byte[1024];
		int len = 0;
		
		while( ( len = fis.read(buffer, 0, 1024) ) != -1 ){
			fos.write(buffer, 0, len);
		}
		
//		Reader reader = new InputStreamReader(new FileReader(inputFile));

        //因为是字符流，所以对应reader
//		BufferedReader br = new BufferedReader(new FileReader(inputFile));
        //包装成buffered
//		
//		PrintWriter pw = new PrintWriter(new FileWriter(outputFile));
//		
//		String temp = "";
//		while( (temp = br.readLine()) != null ) {
//			pw.println(temp);
//		}
//		
//		br.close();
//		pw.close();


		fis.close();
		fos.close();
		
//URLConnection url = new URL
	}

}

```



 >IO按读写划分可以分为输入流和输出流 IO，按处理媒介来划分可以分为字节流和字符流 
 另外为了处理不同的数据类型，输入输出流可以层层包装

字符流有两个抽象类：writer & Reader

对应子类 FileWrite & FlieReader 实现文件读写擦欧总

BufferedWriter & BufferoutputStream 提供缓冲区功能



> 什么时候用字符流？什么时候用字节流？
所谓字符流，肯定是用于操作类似文本文件或者带有字符文件的场合比较多
而字节流则是操作那些无法直接获取文本信息的二进制文件，比如图片，mp3，视频文件等
说白了在硬盘上都是以字节存储的，只不过字符流在操作文本上面更方便一点而已。
采用缓冲区能够在读写大文件的时候有效提高效率
 
 
 
 爬虫实例结合：
 
 
```
 package myfirst;

import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.URL;
import java.util.Iterator;
import java.util.regex.Pattern;
import org.jsoup.Connection;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;
public class imgget {
	public static void main(String[] args) throws IOException {

		String url = "http://movie.nankai.edu.cn/";
		Connection conn = Jsoup.connect(url);
		Document doc = conn.get();
		// System.out.println(doc);
		Elements divelement = doc.getElementsByTag("img");
		int i = 0;
		Iterator<Element> iterator = divelement.iterator();
		while (iterator.hasNext()) {
			Element ele = iterator.next();
			String imgSrc = ele.attr("src");

			String pattern = ".*.jpg.*";
			boolean isMatch = Pattern.matches(pattern, imgSrc);
			if (isMatch) {
				System.out.println(imgSrc);
			}
			
			String address = "http://movie.nankai.edu.cn/" + imgSrc;
			URL url1 = new URL(address);
			InputStream is = url1.openStream();
			byte[] buffer = new byte[1024];
			OutputStream fos = new FileOutputStream("C:\\Users\\mac\\Documents\\java\\" + i + ".jpg");
			
			int len = 0;
			while ((len = is.read(buffer)) != -1) {
				fos.write(buffer, 0, len);
			}

			is.close();
			fos.close();
			i++;
		}
	}
}
```
 




