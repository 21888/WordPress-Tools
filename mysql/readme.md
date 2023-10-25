# 文章相关

## 查询文章的自定义字段是否包函某个字符串
```sql
SELECT p.* 
FROM wp_posts p
JOIN wp_postmeta m ON p.ID = m.post_id 
WHERE m.meta_key = 'key' 
AND m.meta_value LIKE '%value%';
```

## 查询缩略图包函某个字符串 (采集站外链缩略图) -- 使用插件Featured Image from URL (FIFU)的自定义字段
```sql
SELECT p.* 
FROM wp_posts p
JOIN wp_postmeta m ON p.ID = m.post_id 
WHERE m.meta_key = 'fifu_image_url' 
AND m.meta_value LIKE '%strings%';
```


# 标签相关

## 查询所有标签
```sql
SELECT *
FROM wp_terms
WHERE term_id IN (
    SELECT term_id
    FROM wp_term_taxonomy
    WHERE taxonomy = 'post_tag'
		
);
```

## 查询标签列表-包函中文的标签
```sql
SELECT *
FROM wp_terms
WHERE term_id IN (
    SELECT term_id
    FROM wp_term_taxonomy
    WHERE taxonomy = 'post_tag'
		and slug LIKE "\%e%" 
		OR slug LIKE "%\%e%" 
) ;


```
## 查询别名相同的标签列表
```sql
SELECT t1.name as tag_name_1, t2.name as tag_name_2, t1.slug 
FROM wp_terms t1
JOIN wp_terms t2 ON t1.slug = t2.slug
WHERE t1.term_id != t2.term_id
AND t1.term_id IN (
    SELECT term_id
    FROM wp_term_taxonomy
    WHERE taxonomy = 'post_tag'
)
AND t2.term_id IN (
    SELECT term_id
    FROM wp_term_taxonomy
    WHERE taxonomy = 'post_tag'
)
GROUP BY t1.slug
HAVING COUNT(t1.slug) > 1;

```
## 将标签别名转换成拼音
```sql
UPDATE wp_terms 
SET slug = to_pinyin ( NAME ) -- to_pinyin 函数在函数那
WHERE
	term_id IN (
465,501,506,513,524,556,569,589,595,617,620,621,642,647,660,662,663,664,665,676,684,686,687,689,690,702,705,716,766,770,783,785,796,799,837,841,848,855,857,868,869,875,877,879,880,884,886,891,951,953,958,959,960,985,986,987
)
```