# Code Del all product

```
DELETE relations.*, taxes.*, terms.*
FROM ZTViNm_term_relationships AS relations
INNER JOIN ZTViNm_term_taxonomy AS taxes
ON relations.term_taxonomy_id=taxes.term_taxonomy_id
INNER JOIN ZTViNm_terms AS terms
ON taxes.term_id=terms.term_id
WHERE object_id IN (SELECT ID FROM ZTViNm_posts WHERE post_type='product');
 
DELETE FROM ZTViNm_postmeta WHERE post_id IN (SELECT ID FROM ZTViNm_posts WHERE post_type = 'product');
DELETE FROM ZTViNm_posts WHERE post_type = 'product';

DELETE pm FROM ZTViNm_postmeta pm LEFT JOIN ZTViNm_posts wp ON wp.ID = pm.post_id WHERE wp.ID IS NULL;

delete from `ZTViNm_termmeta`
where 
	`term_id` in ( 
		SELECT `term_id`
		FROM `ZTViNm_term_taxonomy`
		WHERE `taxonomy` in ('product_cat', 'product_type', 'product_visibility') 
	);

delete from `ZTViNm_terms`  
where 
	`term_id` in ( 
		SELECT `term_id`
		FROM `ZTViNm_term_taxonomy`
		WHERE `taxonomy` in ('product_cat', 'product_type', 'product_visibility') 
	);
	
DELETE FROM `ZTViNm_term_taxonomy` WHERE `taxonomy` in ('product_cat', 'product_type', 'product_visibility');

DELETE meta FROM ZTViNm_termmeta meta LEFT JOIN ZTViNm_terms terms ON terms.term_id = meta.term_id WHERE terms.term_id IS NULL;

DELETE FROM ZTViNm_woocommerce_attribute_taxonomies;

DELETE FROM ZTViNm_woocommerce_sessions;
```
