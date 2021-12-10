# Python-Pandas-Excecise
Capture Python Case study

wk_exposure=spark.read.format("csv").option("delimiter","|").schema(customschema).option("header","false").load("filepath\ods_wk_exposure_month")
ods_date=spark.read.format("csv").option("delimiter","|").schema(customschema).option("header","false").load("filepath\ods_date_term")
ods_cal=spark.read.format("csv").option("delimiter","|").schema(customschema).option("header","false").load("filepath\ods_calender")

bus_date=spark.read.format("csv").option("delimiter","|").schema(customschema).option("header","false").load("filepath\businsesdates")
cal_date=spark.read.format("csv").option("delimiter","|").schema(customschema).option("header","false").load("filepath\calenderdates")
holiday_df=spark.read.format("csv").option("delimiter","|").schema(customschema).option("header","false").load("filepath\bizcontrolholiday")


wk_exposure.createOrReplaceTempView("wk_exposure_view",false,persistlevel)
ods_date.createOrReplaceTempView("ods_date_view",false,persistlevel)
ods_cal.createOrReplaceTempView("ods_cal_view",false,persistlevel)
bus_date.createOrReplaceTempView("businessdate_view",false,persistlevel)
cal_date.createOrReplaceTempView("calenderdate_view",false,persistlevel)
holiday_df.createOrReplaceTempView("holiday_view",false,persistlevel)


val queryafterrightjoinqry=spark.sql("select "apply same logic" from wk_exposure_view a,ods_date_view b,ods_cal_view c where "same logic" and
b.date_term_cd is not null and "same logic")

val businessdateqry=spark.sql("select "same logic" from businessdate_view")

val holiday_cal=spark.sql("select "samelogic" from holiday_view")

val businessdateqry=spark.sql("select holiday_calender_cd,calender_date,X (select b.calender_cd as holiday_calender_cd,a.calender_date 
as business_date,row number() over(partition by b.calender_cd,a.calender_date 
order by b.calender_cd,a.calender_date) from Calender_dates a join ods_cal_view b where a.calender_date not in("SAT","SUN") and b.calender_payment_flag="Y"))
as temp join holiday_view as t where t.holiday_dt!=calender_date and t.biz_cntr_cd!=b.calender_cd)

