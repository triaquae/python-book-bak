## 本节重点：

* 使学员掌握xml模块的使用

> **本节时长需控制在15分钟内**

xml是实现不同语言或程序之间进行数据交换的协议，跟json差不多，但json使用起来更简单，不过，古时候，在json还没诞生的黑暗年代，大家只能选择用xml呀，至今很多传统公司如金融行业的很多系统的接口还主要是xml。

xml的格式如下，就是通过&lt;&gt;节点来区别数据结构的:

```xml
<?xml version="1.0"?>
<data>
    <country name="Liechtenstein">
        <rank updated="yes">2</rank>
        <year>2008</year>
        <gdppc>141100</gdppc>
        <neighbor name="Austria" direction="E"/>
        <neighbor name="Switzerland" direction="W"/>
    </country>
    <country name="Singapore">
        <rank updated="yes">5</rank>
        <year>2011</year>
        <gdppc>59900</gdppc>
        <neighbor name="Malaysia" direction="N"/>
    </country>
    <country name="Panama">
        <rank updated="yes">69</rank>
        <year>2011</year>
        <gdppc>13600</gdppc>
        <neighbor name="Costa Rica" direction="W"/>
        <neighbor name="Colombia" direction="E"/>
    </country>
</data>
```

xml协议在各个语言里的都 是支持的，在python中可以用以下模块操作xml 　　

```py
import xml.etree.ElementTree as ET
 
tree = ET.parse("xmltest.xml")
root = tree.getroot()
print(root.tag)
 
#遍历xml文档
for child in root:
    print(child.tag, child.attrib)
    for i in child:
        print(i.tag,i.text)
 
#只遍历year 节点
for node in root.iter('year'):
    print(node.tag,node.text)
```

修改和删除xml文档内容

```py
import xml.etree.ElementTree as ET
 
tree = ET.parse("xmltest.xml")
root = tree.getroot()
 
#修改
for node in root.iter('year'):
    new_year = int(node.text) + 1
    node.text = str(new_year)
    node.set("updated","yes")
 
tree.write("xmltest.xml")
 
 
#删除node
for country in root.findall('country'):
   rank = int(country.find('rank').text)
   if rank > 50:
     root.remove(country)
 
tree.write('output.xml')
```

自己创建xml文档

```py
import xml.etree.ElementTree as ET
 
 
new_xml = ET.Element("namelist")
name = ET.SubElement(new_xml,"name",attrib={"enrolled":"yes"})
age = ET.SubElement(name,"age",attrib={"checked":"no"})
sex = ET.SubElement(name,"sex")
sex.text = '33'
name2 = ET.SubElement(new_xml,"name",attrib={"enrolled":"no"})
age = ET.SubElement(name2,"age")
age.text = '19'
 
et = ET.ElementTree(new_xml) #生成文档对象
et.write("test.xml", encoding="utf-8",xml_declaration=True)
 
ET.dump(new_xml) #打印生成的格式
```



