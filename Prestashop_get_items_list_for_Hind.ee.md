## Prestshop SQL query to get items list for DB for hind.ee portal

Set VAT rate, domain name, update DB tables prefixes and shop language prefix (et)

```
use d118895_gate7;
SET @VAT_MULTIPLICATOR = 1.22; # Set VAT rate multiplicator for country of Your residence
SET @SHOP_DOMAIN = 'https://gate7.ee/'; # Set domain name
SELECT SQL_NO_CACHE 
p.id_product as id, pl.name as title, pl.description_short as description
,IF(ISNULL(sp.price), ROUND(p.price * 1.22,2),
IF(sp.price > 0, ROUND(sp.price * (1 - sp.reduction) * @VAT_MULTIPLICATOR, 2), ROUND(p.price * (1 - sp.reduction) * @VAT_MULTIPLICATOR,2))
) as price
,'new' as 'condition', IFNULL(stock.quantity, 0) as stock, p.ean13 as ean_code, p.mpn as manufacturer_code, m.name as manufacturer, '' as model
,CONCAT(@SHOP_DOMAIN,i.id_image,'-large_default/',pl.link_rewrite,'.jpg') as image_url, CONCAT(@SHOP_DOMAIN,'et/',p.id_product,'-',pl.link_rewrite,'-',p.ean13,'.html') as product_url
,p.id_category_default as category_id, cl.name as categroy_name, CONCAT(@SHOP_DOMAIN,'et/',cl.id_category,'-',cl.link_rewrite) as category_link
,0 as delivery_price, 7 as delivery_time
FROM `ps_product` p
INNER JOIN ps_product_shop product_shop ON (product_shop.id_product = p.id_product AND product_shop.id_shop = 1)
INNER JOIN ps_image i ON p.id_product = i.id_product AND cover = 1
INNER JOIN ps_category_lang cl ON  cl.id_category = p.id_category_default AND cl.id_lang = 2
LEFT JOIN ps_specific_price sp on p.id_product = sp.id_product AND sp.from < NOW() AND sp.to > NOW()
LEFT JOIN `ps_product_lang` `pl` ON p.`id_product` = pl.`id_product` AND pl.`id_lang` = 2 AND pl.id_shop = 1 
LEFT JOIN `ps_image_shop` `image_shop` ON image_shop.`id_product` = p.`id_product` AND image_shop.cover=1 AND image_shop.id_shop=1
LEFT JOIN `ps_image_lang` `il` ON image_shop.`id_image` = il.`id_image` AND il.`id_lang` = 2
LEFT JOIN `ps_manufacturer` `m` ON m.`id_manufacturer` = p.`id_manufacturer`
LEFT JOIN ps_stock_available stock ON (stock.id_product = `p`.id_product AND stock.id_product_attribute = 0 AND stock.id_shop = 1  AND stock.id_shop_group = 0  )
WHERE (product_shop.`active` = 1) AND (product_shop.`visibility` IN ("both", "catalog")) AND 
(EXISTS(SELECT 1 FROM `ps_category_product` cp JOIN `ps_category_group` cg ON (cp.id_category = cg.id_category AND cg.`id_group` =1) WHERE cp.`id_product` = p.`id_product`))
ORDER BY product_shop.`date_add` DESC
```

