# hive_to_sas_data
#从hive导数据到sas，数据量不可过大
proc sql;
    %connHdp()  
select * from connection to hadoop (use kumingcheng);
create table saskuming.bussipin_cds_150722 as
select
pin length 40 format $40.,
buy_demand length 8 format 8.,
amount length 8 format 8.,
city length 8 format 8.,
reg_time length 40 format $40.,
user_level length 8 format 8.,
parent_sale_ord_id length 40 format $40.,
item_first_cate_name length 40 format $40.,
item_third_cate_name length 40 format $40.,
item_brand_name length 40 format $40.,
sale_qtty length 8 format 8.,
user_actual_pay_amount length 8 format 8.,
place_ord_ip length 40 format $40.,
dt length 40 format $40.,
intl_ord_flag length 8 format $8.,
cnee_name length 80 format $80.,
cnee_fixed_tel length 40 format $40.,
cnee_mobile_no length 40 format $40.,
rev_addr length 200 format $200.,
orderid length 8 format 8.,
/*orderid应该设置成字符型
orderid length 40 format $40.,*/
ivc_cid length 8 format 8.,
ivc_title length 100 format $100.
from connection to hadoop (
select
pin ,
buy_demand ,
amount ,
city ,
reg_time,
user_level,
parent_sale_ord_id ,
item_first_cate_name,
item_third_cate_name ,
item_brand_name ,
sale_qtty,
user_actual_pay_amount ,
place_ord_ip ,
dt ,
intl_ord_flag ,
regexp_replace(cnee_name,'[^一-龠 !-~]','') as cnee_name,
cnee_fixed_tel ,
cnee_mobile_no ,
regexp_replace(rev_addr,'[^一-龠 !-~]','') as rev_addr,
orderid ,
ivc_cid ,
regexp_replace(ivc_title,'[^一-龠 !-~]','') as ivc_title
from kumingcheng.bussipin_cds_150722);
quit;
