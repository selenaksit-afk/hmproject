
# her Article id tek satır. Article id 'de null değer yok.
# toplam satır sayısı : 105.542
# tekil Article id sayısı : 105.542

SELECT
  COUNT(*) AS total_rows,
  COUNT(DISTINCT article_id) AS unique_articles
FROM `project-c44538cf-504f-4df0-8d6.HM_Project.articles`;

# null kontrolü :
# sadece detail_desc 'te 416 tane eksik veri var. Toplam verinin %0,39'u kadar. Direk null değerleri 'UNKNOWN' olarak değiştirdim.

SELECT
  COUNT(*) AS total_rows,
  COUNTIF(article_id IS NULL) AS null_article_id,
  COUNTIF(product_code IS NULL) AS null_product_code,
  COUNTIF(prod_name IS NULL) AS null_prod_name,
  COUNTIF(product_type_no IS NULL) AS null_product_type_no,
  COUNTIF(product_type_name IS NULL) AS null_product_type_name,
  COUNTIF(product_group_name IS NULL) AS null_product_group_name,
  COUNTIF(graphical_appearance_no IS NULL) AS null_graphical_appearance_no,
  COUNTIF(graphical_appearance_name IS NULL) AS null_graphical_appearance_name,
  COUNTIF(colour_group_code IS NULL) AS null_colour_group_code,
  COUNTIF(colour_group_name IS NULL) AS null_colour_group_name,
  COUNTIF(perceived_colour_value_id IS NULL) AS null_perceived_colour_value_id,
  COUNTIF(perceived_colour_value_name IS NULL) AS null_perceived_colour_value_name,
  COUNTIF(perceived_colour_master_id IS NULL) AS null_perceived_colour_master_id,
  COUNTIF(perceived_colour_master_name IS NULL) AS null_perceived_colour_master_name,
  COUNTIF(department_no IS NULL) AS null_department_no,
  COUNTIF(department_name IS NULL) AS null_department_name,
  COUNTIF(index_code IS NULL) AS null_index_code,
  COUNTIF(index_name IS NULL) AS null_index_name,
  COUNTIF(index_group_no IS NULL) AS null_index_group_no,
  COUNTIF(index_group_name IS NULL) AS null_index_group_name,
  COUNTIF(section_no IS NULL) AS null_section_no,
  COUNTIF(section_name IS NULL) AS null_section_name,
  COUNTIF(garment_group_no IS NULL) AS null_garment_group_no,
  COUNTIF(garment_group_name IS NULL) AS null_garment_group_name,
  COUNTIF(detail_desc IS NULL) AS null_detail_desc

FROM `project-c44538cf-504f-4df0-8d6.HM_Project.articles`;


UPDATE `project-c44538cf-504f-4df0-8d6.HM_Project.articles`
SET detail_desc = 'UNKNOWN'
WHERE detail_desc IS NULL;

SELECT
  COUNTIF(detail_desc IS NULL) AS null_detail_desc
FROM `project-c44538cf-504f-4df0-8d6.HM_Project.articles`;

# Article id ile product id arasındaki ilişki
# Article_id = spesifik ürün varyantı
# product_code = ürün ailesi / model kodu gibi düşünebiliriz. Yani bir product code'un içinde birden fazla Article id mevcut olabilir.

#  Bir product code'un içinde kaç article id mevcut kontrolü:

SELECT
  product_code,
  COUNT(DISTINCT article_id) AS article_count
FROM `project-c44538cf-504f-4df0-8d6.HM_Project.articles`
GROUP BY product_code
ORDER BY article_count DESC
LIMIT 20;

# 783707 product code'un detayı:

SELECT
  product_code,
  article_id,
  prod_name,
  product_type_name,
  product_group_name,
  colour_group_name,
  perceived_colour_master_name,
  department_name,
  index_name,
  index_group_name,
  section_name,
  garment_group_name
FROM `project-c44538cf-504f-4df0-8d6.HM_Project.articles`
WHERE product_code = 783707
ORDER BY article_id;

# Aynı product_code altında bulunan article_id’ler, görünmeyen SKU seviyesinde varyantlar içerebilir.
