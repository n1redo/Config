## Entity

```java
##导入宏定义
$!{define.vm}

##保存文件（宏定义）
#save("/po", ".java")

##包路径（宏定义）
#setPackageSuffix("po")

##自动导入包（全局变量）
$!{autoImport.vm}

import java.io.Serializable;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import com.baomidou.mybatisplus.annotation.TableId;
import com.baomidou.mybatisplus.annotation.TableName;
##表注释（宏定义）
#tableComment("实体类")
@Data
@AllArgsConstructor
@NoArgsConstructor
@TableName("$!{tableInfo.obj.name}")
public class $!{tableInfo.name}  {
#foreach($column in $tableInfo.pkColumn)
    #if(${column.comment})
    /* ${column.comment} */
    #end
    @TableId
    private $!{tool.getClsNameByFullName($column.type)} $!{column.name};
#end
#foreach($column in $tableInfo.otherColumn)
    #if(${column.comment})
    /* ${column.comment} */
#end
    private $!{tool.getClsNameByFullName($column.type)} $!{column.name};
#end
}
```

## Service

```java
##导入宏定义
$!{define.vm}

##设置表后缀（宏定义）
#setTableSuffix("Service")

##保存文件（宏定义）
#save("/service", "Service.java")

##包路径（宏定义）
#setPackageSuffix("service")

import com.baomidou.mybatisplus.extension.service.IService;


##表注释（宏定义）
#tableComment("服务层")
public interface $!{tableName} extends IService<$!tableInfo.name> {

}
```

## ServiceImpl

```java
##导入宏定义
$!{define.vm}

##设置表后缀（宏定义）
#setTableSuffix("ServiceImpl")

##保存文件（宏定义）
#save("/service/impl", "ServiceImpl.java")

##包路径（宏定义）
#setPackageSuffix("service.impl")

import com.baomidou.mybatisplus.extension.service.impl.ServiceImpl;
import org.springframework.stereotype.Service;

##表注释（宏定义）
#tableComment("服务层实现")
@Service("$!tool.firstLowerCase($tableInfo.name)Service")
public class $!{tableName} extends ServiceImpl<$!{tableInfo.name}Mapper, $!{tableInfo.name}> implements $!{tableInfo.name}Service {

}
```

## Dao

```java
##导入宏定义
$!{define.vm}

##设置表后缀（宏定义）
#setTableSuffix("Mapper")

##保存文件（宏定义）
#save("/mapper", "Mapper.java")

##包路径（宏定义）
#setPackageSuffix("mapper")

import com.baomidou.mybatisplus.core.mapper.BaseMapper;
import org.apache.ibatis.annotations.Mapper;

##表注释（宏定义）
#tableComment("数据层")
@Mapper
public interface $!{tableName} extends BaseMapper<$!tableInfo.name> {

}
```