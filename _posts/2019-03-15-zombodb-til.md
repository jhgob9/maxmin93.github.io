
---
title: "Zombodb - pg10 plugin for es6"
date: 2019-03-15 16:00:00 -0000
categories: es til
---

> 출처 : Github [zombodb](https://github.com/zombodb/zombodb)

# Zombodb install

# Zombodb configuration

## zombodb--10-1.0.3.sql

#### CentOS 6 (installed by yum)

PATH `/usr/pgsql-10/share/extension/zombodb--10-1.0.3.sql`

#### Mac OS (installed by brew)

PATH `/usr/local/Cellar/postgresql@10/10.6_1/share/postgresql@10/extension/zombodb--10-1.0.3.sql`

```sql

INSERT INTO analyzers(name, definition, is_default) VALUES (
  'zdb_korean', '{
          "type": "custom",
          "tokenizer": "nori_tokenizer",
          "filter": [
            "lowercase",
            "nori_part_of_speech"
          ]
        }', true);

CREATE DOMAIN text_ko AS text;

-- INSERT INTO type_mappings(type_name, definition, is_default) VALUES (
--   'text', '{
--     "type": "text",
--     "copy_to": "zdb_all",
--     "fielddata": true,
--     "analyzer": "zdb_standard"
--   }', true);

INSERT INTO type_mappings(type_name, definition, is_default) VALUES (
  'text_ko', '{
    "type": "text",
    "copy_to": "zdb_all",
    "analyzer": "zdb_korean"
  }', true);

CREATE DOMAIN korean AS text;      -- nori_analyzer

```


```json
{
	"error":{
		"root_cause":[{
			"type":"mapper_parsing_exception",
			"reason":"analyzer [korean] not found for field [sentence]"
		}],
		"type":"mapper_parsing_exception",
		"reason":"Failed to parse mapping [doc]: analyzer [korean] not found for field [sentence]",
		"caused_by":{
			"type":"mapper_parsing_exception",
			"reason":"analyzer [korean] not found for field [sentence]"
		}
	},
	"status":400
}
```