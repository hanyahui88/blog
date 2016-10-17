---
title: 使用freemarker导出word   
date: 2016-08-05 14:13:35
categories:  技术 
tags: [freemarker,导出,word]
---
1. 先把排版好的word另存为xml格式<br/>
![save as](/path/to/6631564744955828577.png)<br/><!--more-->
2. 然后把替换的内容使用${}标签替换掉，后缀改成ftl，放到项目中。<br/>
3. 代码<br/>

       private static void genWord(Map<String, Object> map) {
            try {
                Configuration configuration = new Configuration(new Version(2, 3, 23));
                configuration.setDefaultEncoding("UTF-8");
                configuration.setClassForTemplateLoading(GenWordUtils.class, "/"); // FTL文件所存在的位置
                Template template = configuration.getTemplate("aa.ftl");
                File outFile = new File("D:/doc/" + map.get("fileName") + ".doc");
                if (!outFile.exists()) {
                    outFile.createNewFile();
                }
                Writer out = new BufferedWriter(new OutputStreamWriter(new FileOutputStream(outFile), "UTF-8"));
                template.process(map, out);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    
        public static void main(String[] args) {
            //需要替换的键值
            Map<String, Object> map = Maps.newHashMap();
            map.put("client", "张三");
            map.put("country", "中国");
            genWord(map);
        }
4. 带有图片的word<br/>
另存xml中的把base64编码的图片替换，${pic}两边不能有空格、换行、制表符......，<br/>

        <w:binData w:name="wordml://${picName}" xml:space="preserve">${pic}</w:binData>
代码和普通的一样，只不过把图片流变成base64编码放进去就可以了<br/>

        BASE64Encoder encoder = new BASE64Encoder();
        map.put("pic", encoder.encode(IOUtils.toByteArray(new FileInputStream("d:/a.jpg"))));