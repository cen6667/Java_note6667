# 1. ElasticSearch概述

![在这里插入图片描述](img/2020090917111970.png#pic_center)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center.png)

# 2. ES与Solr的差别

## 2.1. Solr简介

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-16572742795141.png)

## 2.2. Lucene简介

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-16572742795142.png)

## 2.3. ES VS Solr

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-16572742795153.png)

# 3. ElasticSearch 安装

![在这里插入图片描述](img/20200909173851629.png#pic_center)

[官网](https://www.elastic.co/cn/)

ElasticSearch: https://mirrors.huaweicloud.com/elasticsearch/?C=N&O=D
logstash: https://mirrors.huaweicloud.com/logstash/?C=N&O=D
kibana: https://mirrors.huaweicloud.com/kibana/?C=N&O=D

- 认识目录

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-16572742795154.png)

3. 测试访问

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-16572742795155.png)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-16572742795156.png)



![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70.png)

https://blog.csdn.net/m0_55710969/article/details/121485349



# 4. Kibana安装

开箱即用

配置文件

```yml
server.port: 5601
server.host: "0.0.0.0"
elasticsearch.hosts: ["http://192.168.1.30:9201"]
kibana.index: ".kibana"
i18n.locale: "zh-CN"			# 中文汉化
```

访问测试

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-16572742795157.png)

# 5. ES核心概念

- 索引
- 字段类型（mapping）
- 文档（document）

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-16572742795168.png)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-16572742795169.png)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951610.png)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951611.png)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951612.png)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951613.png)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951614.png)

# 6. IK分词器

- [下载链接]( https://github.com/medcl/elasticsearch-analysis-ik/releases?after=v7.8.0)
- 解压放入到es对应的plugins下即可
- 重启观察ES，发现ik插件被加载了

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951615.png)

- 也可以通过bin目录下elasticsearch-plugin list 查看已经加载的插件

- 使用kibana测试

  - ik_smart: 最少切分

  ![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951616.png)

  - ik_max_word为最细粒度划分！穷尽词库的可能， 字典！

  ![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951617.png)

- ik分词器增加自己的配置！

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951718.png)

- 重启ES 和 Kibana

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951719.png)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951720.png)

# 7. Restful风格说明

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951721.png)

> 基础测试

- 创建一个索引！

```bash
PUT /索引名/~类型名~/文档id
{请求体}

# PUT 创建命令  test1 索引 type1 类型 1 id
PUT test1/type1/1
{
  "name": "xiaofan",
  "age": 28
}

# 返回结果
# 警告信息： 不支持在文档索引请求中的指定类型
# 而是使用无类型的断点(/{index}/_doc/{id}, /{index}/_doc, or /{index}/_create/{id}).
{
  "_index" : "test1",	# 索引
  "_type" : "type1",	# 类型（已经废弃）
  "_id" : "1",			# id
  "_version" : 1,		# 版本
  "result" : "created",	# 操作类型
  "_shards" : {			# 分片信息
    "total" : 2,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 0,
  "_primary_term" : 1
}
```

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951722.png)

- 指定字段的类型（创建规则）

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951723.png)

- 获取具体的索引规则

```bash
# GET test2

{
  "test2" : {
    "aliases" : { },
    "mappings" : {
      "properties" : {
        "age" : {
          "type" : "integer"
        },
        "birthday" : {
          "type" : "date"
        },
        "name" : {
          "type" : "text"
        }
      }
    },
    "settings" : {
      "index" : {
        "creation_date" : "1599708623941",
        "number_of_shards" : "1",
        "number_of_replicas" : "1",
        "uuid" : "ANWnhwArSMSl8k8iipgH1Q",
        "version" : {
          "created" : "7080099"
        },
        "provided_name" : "test2"
      }
    }
  }
}

# 查看默认的规则
PUT /test3/_doc/1
{
  "name": "狂神说Java",
  "age": 28,
  "birthday": "1997-01-05"
}

# GET test3

{
  "test3" : {
    "aliases" : { },
    "mappings" : {
      "properties" : {
        "age" : {
          "type" : "long"
        },
        "birthday" : {
          "type" : "date"
        },
        "name" : {
          "type" : "text",
          "fields" : {
            "keyword" : {
              "type" : "keyword",
              "ignore_above" : 256
            }
          }
        }
      }
    },
    "settings" : {
      "index" : {
        "creation_date" : "1599708906181",
        "number_of_shards" : "1",
        "number_of_replicas" : "1",
        "uuid" : "LzPLCDgeQn6tdKo3xBBpbw",
        "version" : {
          "created" : "7080099"
        },
        "provided_name" : "test3"
      }
    }
  }
}

```

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951724.png)

- 修改索引 POST

```bash
# 只会修改指定项，其他内容保证不变
POST /test3/_doc/1/_update
{
  "doc": {
    "name":"暴徒狂神"
  }
}

# GET test3/_doc/1

{
  "_index" : "test3",
  "_type" : "_doc",
  "_id" : "1",
  "_version" : 2,
  "_seq_no" : 1,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "name" : "暴徒狂神",
    "age" : 28,
    "birthday" : "1997-01-05"
  }
}

```

![在这里插入图片描述](img/20200910115620763.png#pic_center)

# 8. 关于文档的基本操作

- 基本操作（简单的查询）

```bash
put /kuangshen/user/1
{
  "name": "狂神说",
  "age": 23,
  "desc": "一顿操作猛如虎，一看工资2500",
  "tags": ["码农", "技术宅", "直男"]
}

put /kuangshen/user/2
{
  "name": "张三",
  "age": 28,
  "desc": "法外狂徒",
  "tags": ["旅游", "渣男", "交友"]
}

put /kuangshen/user/3
{
  "name": "李四",
  "age": 30,
  "desc": "不知道怎么描述",
  "tags": ["旅游", "靓女", "唱歌"]
}

GET kuangshen/user/1


GET kuangshen/user/_search?q=name:狂神
```



- 复杂操作(排序、分页、高亮、模糊查询、标准查询！)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951725.png)

```bash
# 模糊查询
GET kuangshen/user/_search
{
  "query": {
    "match": {
      "name": "狂神"
    }
  }
}

# 对查询结果进行字段过滤
GET kuangshen/user/_search
{
  "query": {
    "match": {
      "name": "狂神"
    }
  },
  "_source": ["name", "desc"]
}

# 排序
GET kuangshen/user/_search
{
  "query": {
    "match": {
      "name": "狂神"
    }
  },
  "sort":[{
    "age": "asc"
  }]
}

# 分页
GET kuangshen/user/_search
{
  "query": {
    "match": {
      "name": "狂神"
    }
  },
  "sort":[{
    "age": "asc"
  }], 
  "from": 0,
  "size": 2
}
```

> 布尔值条件查询

```bash
# 多条件查询 must 相当于and
GET kuangshen/user/_search
{
  "query": {
    "bool": {
      "must": [
        {"match": {
          "name": "狂神"
        }},
        {"match": {
          "age": 23
        }}
      ]
    }
  }
}

# 多条件查询 should 相当于or
GET kuangshen/user/_search
{
  "query": {
    "bool": {
      "should": [
        {"match": {
          "name": "狂神说"
        }},
        {"match": {
          "age": 25
        }}
      ]
    }
  }
}

# 多条件查询 must_not 相当于 not
GET kuangshen/user/_search
{
  "query": {
    "bool": {
      "must_not": [
        {"match": {
          "age": 25
        }}
      ]
    }
  }
}


# 过滤查询1 age > 24
GET kuangshen/user/_search
{
  "query": {
    "bool": {
      "must": [
        {"match": {
          "name": "狂神"
        }}
      ],
      "filter": [
        {"range": {
          "age": {
            "gt": 24
          }
        }}
      ]
    }
  }
}

# 过滤器2  22<age<30 
GET kuangshen/user/_search
{
  "query": {
    "bool": {
      "must": [
        {"match": {
          "name": "狂神"
        }}
      ],
      "filter": [
        {"range": {
          "age": {
            "lt": 30,
            "gt": 22
          }
        }}
      ]
    }
  }
}
```

> 多条件查询

```bash
GET kuangshen/user/_search
{
  "query": {
    "match": {
      "tags": "技术 男"
    }
  }
}
```

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951726.png)

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951727.png)

> keyword类型不会被分词器解析
>
> term: 精确匹配

```bash
# 定义类型
PUT xiaofan_test_db
{
  "mappings": {
    "properties": {
      "name": {
        "type": "text"
      },
      "desc": {
        "type": "keyword"
      }
    }
  }
}


PUT /xiaofan_test_db/_doc/1
{
  "name": "小范说Java Name",
  "desc": "小范说Java Desc"
}

PUT /xiaofan_test_db/_doc/2
{
  "name": "小范说Java Name",
  "desc": "小范说Java Desc 2"
}

# 按照keyword类型精准匹配
GET xiaofan_test_db/_search
{
  "query": {
    "term": {
      "desc": "小范说Java Desc"
    }
  }
}
# 结果：
{
  "took" : 0,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 0.6931471,
    "hits" : [
      {
        "_index" : "test_db",
        "_type" : "_doc",
        "_id" : "1",
        "_score" : 0.6931471,
        "_source" : {
          "name" : "小范说Java Name",
          "desc" : "小范说Java Desc"
        }
      }
    ]
  }
}

# 按照text类型匹配
GET xiaofan_test_db/_search
{
  "query": {
    "term": {
      "name": "小"
    }
  }
}

# 结果：
{
  "took" : 0,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 2,
      "relation" : "eq"
    },
    "max_score" : 0.18232156,
    "hits" : [
      {
        "_index" : "test_db",
        "_type" : "_doc",
        "_id" : "1",
        "_score" : 0.18232156,
        "_source" : {
          "name" : "小范说Java Name",
          "desc" : "小范说Java Desc"
        }
      },
      {
        "_index" : "test_db",
        "_type" : "_doc",
        "_id" : "2",
        "_score" : 0.18232156,
        "_source" : {
          "name" : "小范说Java Name",
          "desc" : "小范说Java Desc 2"
        }
      }
    ]
  }
}
```

> 多个值匹配精确查询

```bash
PUT /test_db/_doc/3
{
  "t1": "22",
  "t2": "2020-09-10"
}

PUT /test_db/_doc/4
{
  "t1": "33",
  "t2": "2020-09-11"
}

GET test_db/_search
{
  "query": {
    "bool": {
      "should": [
        {
          "term": {
            "t1": "22"
          }
        },
         {
          "term": {
            "t1": "33"
          }
        }
      ]
    }
  }
}
```

> 高亮查询

```bash
GET kuangshen/user/_search
{
  "query": {
    "match": {
      "name": "狂神"
    }
  },
  "highlight": {
    "pre_tags": "<p class='key' style='color:red'>",
    "post_tags": "</p>", 
    "fields": {
      "name": {}
    }
  }
}

# 结果显示：
#! Deprecation: [types removal] Specifying types in search requests is deprecated.
{
  "took" : 1,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 2,
      "relation" : "eq"
    },
    "max_score" : 1.3862942,
    "hits" : [
      {
        "_index" : "kuangshen",
        "_type" : "user",
        "_id" : "1",
        "_score" : 1.3862942,
        "_source" : {
          "name" : "狂神说",
          "age" : 23,
          "desc" : "一顿操作猛如虎，一看工资2500",
          "tags" : [
            "码农",
            "技术宅",
            "直男"
          ]
        },
        "highlight" : {
          "name" : [
            "<p class='key' style='color:red'>狂</p><p class='key' style='color:red'>神</p>说"
          ]
        }
      },
      {
        "_index" : "kuangshen",
        "_type" : "user",
        "_id" : "4",
        "_score" : 1.0892314,
        "_source" : {
          "name" : "狂神说前端",
          "age" : 25,
          "desc" : "大王叫我来巡山",
          "tags" : [
            "码农1",
            "技术宅1",
            "直男1"
          ]
        },
        "highlight" : {
          "name" : [
            "<p class='key' style='color:red'>狂</p><p class='key' style='color:red'>神</p>说前端"
          ]
        }
      }
    ]
  }
}
```

# 9. 集成SpringBoot

- [官网](https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/java-rest-high.html)

- 添加依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
</dependency>
```

- 自定义配置

```java
package com.xiaofan.config;

import org.apache.http.HttpHost;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class ElasticSearchClientConfig {

    @Bean
    public RestHighLevelClient restHighLevelClient() {
        RestHighLevelClient client = new RestHighLevelClient(
            RestClient.builder(
                new HttpHost("192.168.1.30", 9201, "http")
            )
        );

        return client;
    }


}
```

- 编写测试类

```java
package com.xiaofan;

import com.alibaba.fastjson.JSON;
import com.xiaofan.pojo.User;
import org.apache.http.entity.ContentType;
import org.elasticsearch.action.admin.indices.delete.DeleteIndexRequest;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.delete.DeleteRequest;
import org.elasticsearch.action.delete.DeleteResponse;
import org.elasticsearch.action.get.GetRequest;
import org.elasticsearch.action.get.GetResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.index.IndexResponse;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.action.support.master.AcknowledgedResponse;
import org.elasticsearch.action.update.UpdateRequest;
import org.elasticsearch.action.update.UpdateResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.CreateIndexRequest;
import org.elasticsearch.client.indices.CreateIndexResponse;
import org.elasticsearch.client.indices.GetIndexRequest;
import org.elasticsearch.common.unit.TimeValue;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.MatchAllQueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.index.query.TermQueryBuilder;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.elasticsearch.search.fetch.subphase.FetchSourceContext;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.boot.test.context.SpringBootTest;

import java.io.IOException;
import java.util.ArrayList;
import java.util.concurrent.TimeUnit;

@SpringBootTest
class EsApiApplicationTests {

	public static final String INDEX = "xiaofan_test_index";

	@Autowired
	@Qualifier(value = "restHighLevelClient")
	private RestHighLevelClient client;

	// 创建索引
	@Test
	void testCreateIndex() throws IOException {
		// 1. 创建索引请求
		CreateIndexRequest request = new CreateIndexRequest(INDEX);
		// 2. 客户端执行请求， IndicesClient，请求后获得响应
		CreateIndexResponse createIndexResponse = client.indices().create(request, RequestOptions.DEFAULT);
		System.out.println(createIndexResponse);
	}

	// 测试索引存在
	@Test
	void testExistsIndex() throws IOException {
		GetIndexRequest request = new GetIndexRequest(INDEX);
		boolean exists = client.indices().exists(request, RequestOptions.DEFAULT);
		System.out.println(exists);
	}

	// 删除索引
	@Test
	void testDeleteIndex() throws IOException {
		DeleteIndexRequest request = new DeleteIndexRequest(INDEX);
		AcknowledgedResponse acknowledgedResponse = client.indices().delete(request, RequestOptions.DEFAULT);
		System.out.println(acknowledgedResponse.isAcknowledged());
	}

	// 添加文档
	@Test
	void testAddDocument() throws IOException {
		User user = new User("狂神说", 28);
		IndexRequest request = new IndexRequest(INDEX);
		// 规则 PUT /index/_doc/1
		request.id("1");
		request.timeout(TimeValue.timeValueSeconds(1));
		// 将数据放入请求 json
		request.source(JSON.toJSONString(user), XContentType.JSON);
		IndexResponse response = client.index(request, RequestOptions.DEFAULT);
		System.out.println(response.toString());
		System.out.println(response.status());
	}

	// 获取文档 判断是否存在 GET /index/_doc/1
	@Test
	void testIsExists() throws IOException {
		GetRequest request = new GetRequest(INDEX, "1");
		// 不获取返回的 _source 的上下文了
		request.fetchSourceContext(new FetchSourceContext(false));
		request.storedFields("_none_");

		boolean exists = client.exists(request, RequestOptions.DEFAULT);
		System.out.println(exists);
	}

	// 获取文档

	/**
	 * 返回结果：
	 * {"age":28,"name":"狂神说"}
	 * {"_index":"xiaofan_test_index","_type":"_doc","_id":"1","_version":1,"_seq_no":0,"_primary_term":1,"found":true,"_source":{"age":28,"name":"狂神说"}}
	 */
	@Test
	void testGetDocument() throws IOException {
		GetRequest request = new GetRequest(INDEX, "1");
		GetResponse response = client.get(request, RequestOptions.DEFAULT);
		System.out.println(response.getSourceAsString());
		System.out.println(response);
	}

	// 更新文档
	@Test
	void testUpdateDocument() throws IOException {
		UpdateRequest request = new UpdateRequest(INDEX, "1");
		request.timeout("1s");

		User user = new User("小范说Java", 18);
		request.doc(JSON.toJSONString(user), XContentType.JSON);

		UpdateResponse updateResponse = client.update(request, RequestOptions.DEFAULT);
		System.out.println(updateResponse);
	}

	// 删除文档
	@Test
	void testDeleteDocument() throws IOException {
		DeleteRequest request = new DeleteRequest(INDEX, "1");
		request.timeout("1s");

		DeleteResponse deleteResponse = client.delete(request, RequestOptions.DEFAULT);
		System.out.println(deleteResponse);

	}

	// 批量插入数据（修改，删除类似操作）
	@Test
	void testBulkRequest() throws IOException {
		BulkRequest request = new BulkRequest();
		request.timeout("10s");

		ArrayList<User> users = new ArrayList<>();
		users.add(new User("kuangshen1", 21));
		users.add(new User("kuangshen2", 22));
		users.add(new User("kuangshen3", 23));
		users.add(new User("xiaofan1", 18));
		users.add(new User("xiaofan2", 19));

		// 批处理请求， 修改，删除，只要在这里修改相应的请求就可以
		for (int i = 0; i < users.size(); i++) {
			request.add(new IndexRequest(INDEX)
					.id(String.valueOf(i + 1))
					.source(JSON.toJSONString(users.get(i)), XContentType.JSON));
		}

		BulkResponse bulkResponse = client.bulk(request, RequestOptions.DEFAULT);
		//是否失败，返回false表示成功
		System.out.println(bulkResponse.hasFailures());
	}

	// 查询文档
	@Test
	void testSearch() throws IOException {
		SearchRequest searchRequest = new SearchRequest(INDEX);
		// 构建搜索条件
		SearchSourceBuilder sourceBuilder = new SearchSourceBuilder();

		// 查询条件， 可以使用QueryBuilders工具类实现
		// QueryBuilders.termQuery 精确
		// QueryBuilders.matchLLQuery() 匹配所有
		TermQueryBuilder termQueryBuilder = QueryBuilders.termQuery("name", "kuangshen1");
		// MatchAllQueryBuilder matchAllQueryBuilder = QueryBuilders.matchAllQuery();
		sourceBuilder.query(termQueryBuilder);
		sourceBuilder.timeout(new TimeValue(60, TimeUnit.SECONDS));

		searchRequest.source(sourceBuilder);

		SearchResponse searchResponse = client.search(searchRequest, RequestOptions.DEFAULT);
		System.out.println(JSON.toJSON(searchResponse.getHits()));
		System.out.println("======================================");
		for (SearchHit documentFields : searchResponse.getHits().getHits()) {
			System.out.println(documentFields.getSourceAsMap());
		}

	}

}
```



# 10. 实战：模拟全文搜索-京东搜索

- github链接：https://github.com/fanjianhai/CODE/tree/main/SpringBoot/springboot-11-elasticsearch-jd

- 搭建springboot项目，添加依赖，修改es版本

```xml
<properties>
    <java.version>1.8</java.version>
    <elasticsearch.version>7.9.2</elasticsearch.version>
</properties>

<dependencies>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.73</version>
    </dependency>
    <dependency>
        <groupId>org.jsoup</groupId>
        <artifactId>jsoup</artifactId>
        <version>1.13.1</version>
    </dependency>
</dependencies>
```

- 整体效果

![在这里插入图片描述](img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center-165727427951828.png)

