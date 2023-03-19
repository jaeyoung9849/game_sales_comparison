-- 게임별, 가입날짜별(일별) 가입인원수
with A as (
select regdate_kst, count(*) as cnt_a
from userinfo
where game_id = 'A'
group by regdate_kst
order by regdate_kst
),
B as (
select regdate_kst, count(*) as cnt_b
from userinfo
where game_id = 'B'
group by regdate_kst
order by regdate_kst
)
select *
from A as AA
join B as BB
on AA.regdate_kst = BB.regdate_kst;
-- 게임별, 가입날짜별(일별) 가입인원수
select game_id, regdate_kst, count(*) as cnt
from userinfo
group by game_id, regdate_kst
order by game_id, regdate_kst;



-- 게임별, 가입날짜별(월별) 가입인원수
with A as (
select date_trunc('month', regdate_kst)::date as mon, count(*) as cnt_a
from userinfo
where game_id = 'A'
group by date_trunc('month', regdate_kst)::date
order by mon
),
B as (
select date_trunc('month', regdate_kst)::date as mon, count(*) as cnt_b
from userinfo
where game_id = 'B'
group by date_trunc('month', regdate_kst)::date
order by mon
)
select *
from A as AA
join B as BB
on AA.mon = BB.mon;
-- 게임별, 가입날짜별(월별) 가입인원수
select game_id, date_trunc('month', regdate_kst)::date as mon, count(*) as cnt
from userinfo
group by game_id, date_trunc('month', regdate_kst)::date 
order by game_id, mon;



-- 게임별, 첫 접속 당시 국가별 가입인원수
with A as (
select geo as geo_a, count(*) as cnt_a
from userinfo
where game_id = 'A'
group by geo
order by geo
),
B as (
select geo as geo_b, count(*) as cnt_b
from userinfo
where game_id = 'B'
group by geo
order by geo
)
select *
from A as AA
join B as BB
on AA.geo_a = BB.geo_b;
-- 게임별, 첫 접속 당시 국가별 가입인원수
select game_id, geo, count(*) as cnt
from userinfo
group by game_id, geo
order by game_id, cnt desc;



-- 게임별, 첫 접속 당시 매체별 가입인원수
with A as (
select media, count(*) as cnt_a
from userinfo
where game_id = 'A'
group by media
order by media
),
B as (
select media, count(*) as cnt_b
from userinfo
where game_id = 'B'
group by media
order by media
)
select *
from A as AA
join B as BB
on AA.media = BB.media;
-- 게임별, 첫 접속 당시 매체별 가입인원수
select game_id, media, count(*) as cnt
from userinfo
group by game_id, media
order by game_id, cnt desc;



-- 게임별, 첫 접속 당시 os별 가입인원수
with A as (
select os, count(*) as cnt_a
from userinfo
where game_id = 'A'
group by os
order by os
),
B as (
select os, count(*) as cnt_b
from userinfo
where game_id = 'B'
group by os
order by os
)
select *
from A as AA
join B as BB
on AA.os = BB.os;
-- 게임별, 첫 접속 당시 os별 가입인원수
select game_id, os, count(*) as cnt
from userinfo
group by game_id, os
order by game_id, cnt desc;



-- 게임별, 나라별, 미디어별 가입자수
select game_id, geo, media, count(*) as cnt
from userinfo
group by game_id, geo, media
order by game_id, geo, cnt desc;


-- 게임별, 운영체제별, 미디어별 가입자수
select game_id, os, media, count(*) as cnt
from userinfo
group by game_id, os, media
order by game_id, os, cnt desc;

---------------------------------------------------------------
-- 게임별, 구매마켓별 매출액(전체기간 : 2020.10.01 ~ 2021.01.31)
select game_id, market_code, sum(price)
from purchase
group by game_id, market_code;


-- 게임별, 구매마켓별, 월별 매출액
with A as (
select game_id, market_code, date_trunc('month', logtime_kst)::date as mon, sum(price) 
from purchase
where game_id = 'A'
group by game_id, market_code, date_trunc('month', logtime_kst)::date
order by market_code, mon
),
B as (
select game_id, market_code, date_trunc('month', logtime_kst)::date as mon, sum(price) 
from purchase
where game_id = 'B'
group by game_id, market_code, date_trunc('month', logtime_kst)::date
order by market_code, mon
)
select *
from A as AA
left join B as BB
on AA.market_code = BB.market_code
and AA.mon = BB.mon;


-- 게임별, 월별 결제자수(같은 유저가 여러달에 결제할 수 있음)
with A as (
select date_trunc('month', logdate_kst)::date as mon , count(distinct(userkey)) as cnt_a
from purchase
where game_id = 'A'
group by date_trunc('month', logdate_kst)::date
order by mon
),
B as (
select date_trunc('month', logdate_kst)::date as mon , count(distinct(userkey)) as cnt_b
from purchase
where game_id = 'B'
group by date_trunc('month', logdate_kst)::date
order by mon
)
select *
from A as AA
join B as BB
on AA.mon = BB.mon;


-- 게임별, 구매마켓별 팔린 상품의 갯수
with A as (
select game_id, market_code, count(distinct(package_name))
from purchase
where game_id = 'A'
group by game_id, market_code
order by market_code
),
B as (
select game_id, market_code, count(distinct(package_name))
from purchase
where game_id = 'B'
group by game_id, market_code
order by market_code
)
select *
from A as AA
left join B as BB
on AA.market_code = BB.market_code;


-- A게임 마켓별 중복되는 상품 있나 확인
with A as (
select *
from purchase
where game_id = 'A'
and market_code = '2'
),
B as (
select *
from purchase
where game_id ='A'
and market_code = '5'
)
select *
from A as AA
join B as BB
on AA.package_name = BB.package_name;


-- 게임별, 마켓별 매출액 & 팔린상품의갯수
select game_id, market_code, sum(price) as total_sum, count(*) as cnt
from purchase
group by game_id, market_code
order by game_id, market_code, total_sum desc; 


-- 게임별 매출액 & 구매유저수 (월별)
select game_id, date_trunc('month', logdate_kst)::date as mon, sum(price) as total_sum, count(distinct(userkey)) as cnt
from purchase
group by game_id, date_trunc('month', logdate_kst)::date
order by game_id, mon;


-- 게임별, 마켓별 매축액 & 팔린상품의갯수 (월별)
select game_id, market_code, date_trunc('month', logdate_kst)::date as mon, sum(price) as total_sum, count(*) as cnt 
from purchase
group by game_id, market_code, date_trunc('month', logdate_kst)::date
order by game_id, market_code, mon;


-- 게임별, 마켓별 매축액 & 팔린상품의갯수 (일별)
select game_id, market_code, date_trunc('day', logdate_kst)::date as day, sum(price) as total_sum, count(*) as cnt 
from purchase
group by game_id, market_code, date_trunc('day', logdate_kst)::date
order by game_id, market_code, day;


-- 게임별, 마켓별, 상품별, 매출액 & 팔린상품의갯수
select game_id, market_code, package_name, sum(price) as total_sum, count(*) as cnt
from purchase
group by game_id, market_code, package_name
order by game_id, market_code, total_sum desc;


-- A게임과 B게임을 동시에 즐기는 유저 찾아보기
with A as (
select *
from purchase
where game_id = 'A'
),
B as (
select *
from purchase
where game_id ='B'
)
select *
from A as AA
join B as BB
on AA.userkey = BB.userkey;


-- A게임의 1, 2번마켓을 동시에 이용하는 유저 찾아보기
with A as (
select *
from purchase
where game_id = 'A'
and market_code = '1'
),
B as (
select *
from purchase
where game_id ='A'
and market_code = '2'
)
select *
from A as AA
join B as BB
on AA.userkey = BB.userkey
and AA.logdate_kst = BB.logdate_kst;


-- A게임에서 돈을 많이쓴 유저순으로 보기(전체기간 : 2020.10.01 ~ 2021.01.31)
select game_id, userkey, sum(price) as total_sum
from purchase
where game_id = 'A'
group by game_id, userkey
order by total_sum desc;


-- 1900.01.01 가입자 정보 확인해보기(정렬을 가입날짜순으로 해서)
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
order by A.regdate_kst;


---------------------------------------------------------
-- A게임 전체기간 PUR 구하기(0.0101)
with tmp as (
select A.game_id as game_id_a, A.userkey as userkey_a, A.geo as geo_a,
B.game_id as game_id_b, B.userkey as userkey_b, B.market_code as market_code_b, B.price as price_b
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'A'
)
select round (count(distinct(userkey_b))::numeric  / count(distinct(userkey_a))::numeric , 4) as pur
from tmp;


-- B게임 전체기간 PUR 구하기(0.0137)
with tmp as (
select A.userkey as userkey_a, A.geo as geo_a,
B.userkey as userkey_b, B.price as price_b
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'B'
)
select round (count(distinct(userkey_b))::numeric  / count(distinct(userkey_a))::numeric , 4) as pur
from tmp;


-- B게임 2020.10.31이후 가입자의 PUR 구하기(0.0103)
with tmp as (
select A.userkey as userkey_a, A.geo as geo_a,
B.userkey as userkey_b, B.price as price_b
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'B'
and A.regdate_kst > '2020-10-31'
)
select round (count(distinct(userkey_b))::numeric  / count(distinct(userkey_a))::numeric , 4) as pur
from tmp;


-- A게임의 ARPU (전체기간) (3089.38)
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'A'
)
select round( (sum(price) / count(distinct(userkey_a))::numeric), 2) as ARPU
from tmp;


-- B게임의 ARPU (전체기간) (3588.36)
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'B'
)
select round( (sum(price) / count(distinct(userkey_a))::numeric), 2) as ARPU
from tmp;


-- A게임의 월별 ARPU (가입일 기준)
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'A'
)
select game_id, date_trunc('month', regdate_kst)::date as mon, sum(price) as rev, 
count(distinct(userkey_a)) as cnt, round( (sum(price)/count(distinct(userkey_a))::numeric), 2) as ARPU
from tmp
group by game_id, date_trunc('month', regdate_kst)::date;


-- A게임과 B게임의 월별 ARPU (가입일 기준)
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
)
select game_id, date_trunc('month', regdate_kst)::date as mon, sum(price) as rev, 
count(distinct(userkey_a)) as cnt, round( (sum(price)/count(distinct(userkey_a))::numeric), 2) as ARPU
from tmp
group by game_id, date_trunc('month', regdate_kst)::date;


-- 게임별, 월별 매출액 & 가입자수 구하기
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
)
select game_id, date_trunc('month', regdate_kst)::date as mon, sum(price) as total_sum, count(distinct(userkey_a)) as cnt
from tmp
group by game_id, date_trunc('month', regdate_kst)::date


-- 게임별, ARPPU (전체기간)
select game_id, sum(price) as total_sum, count(distinct(userkey)) as cnt,
round( sum(price)/count(distinct(userkey))::numeric , 2) as ARPPU
from purchase
group by game_id
order by game_id;


-- 게임별, 월별 ARPPU (구매일 기준)
select game_id, date_trunc('month', logdate_kst)::date as mon, sum(price) as total_sum, count(distinct(userkey)) as cnt,
round( sum(price)/count(distinct(userkey))::numeric , 2) as ARPPU
from purchase
group by game_id, date_trunc('month', logdate_kst)::date
order by game_id, mon;




-------------------------------------------------------------------------
---------------------------------------------------------------------------


---------------------------------------------------------
-- A게임 전체기간 PUR 구하기(0.0101)
with tmp as (
select A.game_id as game_id_a, A.userkey as userkey_a, A.geo as geo_a,
B.game_id as game_id_b, B.userkey as userkey_b, B.market_code as market_code_b, B.price as price_b
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'A'
)
select count(distinct(userkey_b)) as paying_users_a,
count(distinct(userkey_a)) as total_users_a,
round (count(distinct(userkey_b))::numeric  / count(distinct(userkey_a))::numeric , 4) as pur_a
from tmp;


-- B게임 전체기간 PUR 구하기(0.0137)
with tmp as (
select A.userkey as userkey_a, A.geo as geo_a,
B.userkey as userkey_b, B.price as price_b
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'B'
)
select count(distinct(userkey_b)) as paying_users_b,
count(distinct(userkey_a)) as total_users_b,
round (count(distinct(userkey_b))::numeric  / count(distinct(userkey_a))::numeric , 4) as pur_b
from tmp;


-- B게임 2020.10.31이후 가입자의 PUR 구하기(0.0103)
with tmp as (
select A.userkey as userkey_a, A.geo as geo_a,
B.userkey as userkey_b, B.price as price_b
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'B'
and A.regdate_kst > '2020-10-31'
)
select round (count(distinct(userkey_b))::numeric  / count(distinct(userkey_a))::numeric , 4) as pur
from tmp;


-- A게임의 ARPU (전체기간) (3089.38)
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'A'
)
select sum(price) as total_sum_a, count(distinct(userkey_a)) as total_user_a,
round( (sum(price) / count(distinct(userkey_a))::numeric), 2) as ARPU_a
from tmp;


-- B게임의 ARPU (전체기간) (3588.36)
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'B'
)
select sum(price) as total_sum_b, count(distinct(userkey_a)) as total_user_b,
round( (sum(price) / count(distinct(userkey_a))::numeric), 2) as ARPU_b
from tmp;


-- A게임의 월별 ARPU (가입일 기준)
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'A'
)
select game_id, date_trunc('month', regdate_kst)::date as mon, sum(price) as rev, 
count(distinct(userkey_a)) as cnt, round( (sum(price)/count(distinct(userkey_a))::numeric), 2) as ARPU_a
from tmp
group by game_id, date_trunc('month', regdate_kst)::date;


-- A게임과 B게임의 월별 ARPU (가입일 기준)
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
)
select game_id, date_trunc('month', regdate_kst)::date as mon, sum(price) as rev, 
count(distinct(userkey_a)) as cnt, round( (sum(price)/count(distinct(userkey_a))::numeric), 2) as ARPU
from tmp
group by game_id, date_trunc('month', regdate_kst)::date;


-- 게임별, 월별 매출액 & 가입자수 구하기
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
)
select game_id, date_trunc('month', regdate_kst)::date as mon, sum(price) as total_sum, count(distinct(userkey_a)) as cnt
from tmp
group by game_id, date_trunc('month', regdate_kst)::date


-- 게임별, ARPPU (전체기간)
select game_id, sum(price) as total_sum, count(distinct(userkey)) as cnt,
round( sum(price)/count(distinct(userkey))::numeric , 2) as ARPPU
from purchase
group by game_id
order by game_id;


-- 게임별, 월별 ARPPU (구매일 기준)
select game_id, date_trunc('month', logdate_kst)::date as mon, sum(price) as total_sum, count(distinct(userkey)) as cnt,
round( sum(price)/count(distinct(userkey))::numeric , 2) as ARPPU
from purchase
group by game_id, date_trunc('month', logdate_kst)::date
order by game_id, mon;



-- 리텐션 분석
-- A게임의 신규가입자당 평균 매출 (월별 리텐션)
with tmp_01 as (
select u.userkey, date_trunc('month', u.regdate_kst)::date as user_regdate, date_trunc('month', p.logdate_kst)::date as user_logdate, sum(p.price) as total_price
from userinfo as u
left join purchase as p 
on u.userkey = p.userkey
where u.game_id = 'A'
and (u.regdate_kst >= '2020-10-01' and u.regdate_kst <= '2021-01-31')
group by u.userkey, date_trunc('month', u.regdate_kst)::date, date_trunc('month', p.logdate_kst)::date
),
tmp_02 as (
select user_regdate, count(distinct(userkey)) as cnt,
sum(case when user_logdate = user_regdate then total_price else null end ) as m0_sum,
sum(case when user_logdate = user_regdate + interval '1 month' then total_price else null end ) as m1_sum,
sum(case when user_logdate = user_regdate + interval '2 month' then total_price else null end ) as m2_sum,
sum(case when user_logdate = user_regdate + interval '3 month' then total_price else null end ) as m3_sum
from tmp_01
group by user_regdate
order by user_regdate
)
select user_regdate, cnt,
round(m0_sum/cnt, 0) as m0,
round(m1_sum/cnt, 0) as m1,
round(m2_sum/cnt, 0) as m2,
round(m3_sum/cnt, 0) as m3
from tmp_02 
order by user_regdate;


-- B게임의 신규가입자당 평균 매출 (월별 리텐션)
with tmp_01 as (
select u.userkey, date_trunc('month', u.regdate_kst)::date as user_regdate, date_trunc('month', p.logdate_kst)::date as user_logdate, sum(p.price) as total_price
from userinfo as u
left join purchase as p 
on u.userkey = p.userkey
where u.game_id = 'B'
and (u.regdate_kst >= '2020-10-01' and u.regdate_kst <= '2021-01-31')
group by u.userkey, date_trunc('month', u.regdate_kst)::date, date_trunc('month', p.logdate_kst)::date
),
tmp_02 as (
select user_regdate, count(distinct(userkey)) as cnt,
sum(case when user_logdate = user_regdate then total_price else null end ) as m0_sum,
sum(case when user_logdate = user_regdate + interval '1 month' then total_price else null end ) as m1_sum,
sum(case when user_logdate = user_regdate + interval '2 month' then total_price else null end ) as m2_sum,
sum(case when user_logdate = user_regdate + interval '3 month' then total_price else null end ) as m3_sum
from tmp_01
group by user_regdate
order by user_regdate
)
select user_regdate, cnt,
round(m0_sum/cnt, 0) as m0,
round(m1_sum/cnt, 0) as m1,
round(m2_sum/cnt, 0) as m2,
round(m3_sum/cnt, 0) as m3
from tmp_02 
order by user_regdate;


-- A게임의 구매자당 평균 매출 (월별 리텐션)
with tmp_01 as (
select userkey, min(logdate_kst) as first_date
from purchase
group by userkey
),
tmp_02 as (
select a.*, b.first_date
from purchase a
left join tmp_01 b
on a.userkey = b.userkey
),
tmp_03 as (
select userkey, date_trunc('month', first_date)::date as first_date, date_trunc('month', logdate_kst)::date as user_logdate, sum(price) as total_price
from tmp_02
where game_id = 'A'
group by userkey, date_trunc('month', first_date)::date, date_trunc('month', logdate_kst)::date
order by userkey
),
tmp_04 as (
select first_date, count(distinct(userkey)) as cnt,
sum(case when user_logdate = first_date then total_price else null end ) as m0_sum,
sum(case when user_logdate = first_date + interval '1 month' then total_price else null end ) as m1_sum,
sum(case when user_logdate = first_date + interval '2 month' then total_price else null end ) as m2_sum,
sum(case when user_logdate = first_date + interval '3 month' then total_price else null end ) as m3_sum
from tmp_03
group by first_date
order by first_date
)
select first_date, cnt,
round(m0_sum/cnt, 0) as m0,
round(m1_sum/cnt, 0) as m1,
round(m2_sum/cnt, 0) as m2,
round(m3_sum/cnt, 0) as m3
from tmp_04 
order by first_date;




-- B게임의 구매자당 평균 매출 (월별 리텐션)
with tmp_01 as (
select userkey, min(logdate_kst) as first_date
from purchase
group by userkey
),
tmp_02 as (
select a.*, b.first_date
from purchase a
left join tmp_01 b
on a.userkey = b.userkey
),
tmp_03 as (
select userkey, date_trunc('month', first_date)::date as first_date, date_trunc('month', logdate_kst)::date as user_logdate, sum(price) as total_price
from tmp_02
where game_id = 'B'
group by userkey, date_trunc('month', first_date)::date, date_trunc('month', logdate_kst)::date
order by userkey
),
tmp_04 as (
select first_date, count(distinct(userkey)) as cnt,
sum(case when user_logdate = first_date then total_price else null end ) as m0_sum,
sum(case when user_logdate = first_date + interval '1 month' then total_price else null end ) as m1_sum,
sum(case when user_logdate = first_date + interval '2 month' then total_price else null end ) as m2_sum,
sum(case when user_logdate = first_date + interval '3 month' then total_price else null end ) as m3_sum
from tmp_03
group by first_date
order by first_date
)
select first_date, cnt,
round(m0_sum/cnt, 0) as m0,
round(m1_sum/cnt, 0) as m1,
round(m2_sum/cnt, 0) as m2,
round(m3_sum/cnt, 0) as m3
from tmp_04 
order by first_date;


-- A게임의 신규가입자당 평균 매출 (주별 리텐션)
with tmp_01 as (
select u.userkey, date_trunc('week', u.regdate_kst)::date as user_regdate, date_trunc('week', p.logdate_kst)::date as user_logdate, sum(p.price) as total_price
from userinfo as u
left join purchase as p 
on u.userkey = p.userkey
where u.game_id = 'A'
and (u.regdate_kst >= '2020-10-05' and u.regdate_kst <= '2021-02-01')
group by u.userkey, date_trunc('week', u.regdate_kst)::date, date_trunc('week', p.logdate_kst)::date
),
tmp_02 as (
select user_regdate, count(distinct(userkey)) as cnt,
sum(case when user_logdate = user_regdate then total_price else null end ) as w0_sum,
sum(case when user_logdate = user_regdate + interval '1 week' then total_price else null end ) as w1_sum,
sum(case when user_logdate = user_regdate + interval '2 week' then total_price else null end ) as w2_sum,
sum(case when user_logdate = user_regdate + interval '3 week' then total_price else null end ) as w3_sum,
sum(case when user_logdate = user_regdate + interval '4 week' then total_price else null end ) as w4_sum,
sum(case when user_logdate = user_regdate + interval '5 week' then total_price else null end ) as w5_sum,
sum(case when user_logdate = user_regdate + interval '6 week' then total_price else null end ) as w6_sum,
sum(case when user_logdate = user_regdate + interval '7 week' then total_price else null end ) as w7_sum,
sum(case when user_logdate = user_regdate + interval '8 week' then total_price else null end ) as w8_sum,
sum(case when user_logdate = user_regdate + interval '9 week' then total_price else null end ) as w9_sum,
sum(case when user_logdate = user_regdate + interval '10 week' then total_price else null end ) as w10_sum,
sum(case when user_logdate = user_regdate + interval '11 week' then total_price else null end ) as w11_sum,
sum(case when user_logdate = user_regdate + interval '12 week' then total_price else null end ) as w12_sum,
sum(case when user_logdate = user_regdate + interval '13 week' then total_price else null end ) as w13_sum,
sum(case when user_logdate = user_regdate + interval '14 week' then total_price else null end ) as w14_sum,
sum(case when user_logdate = user_regdate + interval '15 week' then total_price else null end ) as w15_sum,
sum(case when user_logdate = user_regdate + interval '16 week' then total_price else null end ) as w16_sum
from tmp_01
group by user_regdate
order by user_regdate
)
select user_regdate, cnt,
round(w0_sum/cnt, 0) as w0,
round(w1_sum/cnt, 0) as w1,
round(w2_sum/cnt, 0) as w2,
round(w3_sum/cnt, 0) as w3,
round(w4_sum/cnt, 0) as w4,
round(w5_sum/cnt, 0) as w5,
round(w6_sum/cnt, 0) as w6,
round(w7_sum/cnt, 0) as w7,
round(w8_sum/cnt, 0) as w8,
round(w9_sum/cnt, 0) as w9,
round(w10_sum/cnt, 0) as w10,
round(w11_sum/cnt, 0) as w11,
round(w12_sum/cnt, 0) as w12,
round(w13_sum/cnt, 0) as w13,
round(w14_sum/cnt, 0) as w14,
round(w15_sum/cnt, 0) as w15,
round(w16_sum/cnt, 0) as w16
from tmp_02 
order by user_regdate;



-- B게임의 신규가입자당 평균 매출 (주별 리텐션)
with tmp_01 as (
select u.userkey, date_trunc('week', u.regdate_kst)::date as user_regdate, date_trunc('week', p.logdate_kst)::date as user_logdate, sum(p.price) as total_price
from userinfo as u
left join purchase as p 
on u.userkey = p.userkey
where u.game_id = 'B'
and (u.regdate_kst >= '2020-10-05' and u.regdate_kst <= '2021-02-01')
group by u.userkey, date_trunc('week', u.regdate_kst)::date, date_trunc('week', p.logdate_kst)::date
),
tmp_02 as (
select user_regdate, count(distinct(userkey)) as cnt,
sum(case when user_logdate = user_regdate then total_price else null end ) as w0_sum,
sum(case when user_logdate = user_regdate + interval '1 week' then total_price else null end ) as w1_sum,
sum(case when user_logdate = user_regdate + interval '2 week' then total_price else null end ) as w2_sum,
sum(case when user_logdate = user_regdate + interval '3 week' then total_price else null end ) as w3_sum,
sum(case when user_logdate = user_regdate + interval '4 week' then total_price else null end ) as w4_sum,
sum(case when user_logdate = user_regdate + interval '5 week' then total_price else null end ) as w5_sum,
sum(case when user_logdate = user_regdate + interval '6 week' then total_price else null end ) as w6_sum,
sum(case when user_logdate = user_regdate + interval '7 week' then total_price else null end ) as w7_sum,
sum(case when user_logdate = user_regdate + interval '8 week' then total_price else null end ) as w8_sum,
sum(case when user_logdate = user_regdate + interval '9 week' then total_price else null end ) as w9_sum,
sum(case when user_logdate = user_regdate + interval '10 week' then total_price else null end ) as w10_sum,
sum(case when user_logdate = user_regdate + interval '11 week' then total_price else null end ) as w11_sum,
sum(case when user_logdate = user_regdate + interval '12 week' then total_price else null end ) as w12_sum,
sum(case when user_logdate = user_regdate + interval '13 week' then total_price else null end ) as w13_sum,
sum(case when user_logdate = user_regdate + interval '14 week' then total_price else null end ) as w14_sum,
sum(case when user_logdate = user_regdate + interval '15 week' then total_price else null end ) as w15_sum,
sum(case when user_logdate = user_regdate + interval '16 week' then total_price else null end ) as w16_sum
from tmp_01
group by user_regdate
order by user_regdate
)
select user_regdate, cnt,
round(w0_sum/cnt, 0) as w0,
round(w1_sum/cnt, 0) as w1,
round(w2_sum/cnt, 0) as w2,
round(w3_sum/cnt, 0) as w3,
round(w4_sum/cnt, 0) as w4,
round(w5_sum/cnt, 0) as w5,
round(w6_sum/cnt, 0) as w6,
round(w7_sum/cnt, 0) as w7,
round(w8_sum/cnt, 0) as w8,
round(w9_sum/cnt, 0) as w9,
round(w10_sum/cnt, 0) as w10,
round(w11_sum/cnt, 0) as w11,
round(w12_sum/cnt, 0) as w12,
round(w13_sum/cnt, 0) as w13,
round(w14_sum/cnt, 0) as w14,
round(w15_sum/cnt, 0) as w15,
round(w16_sum/cnt, 0) as w16
from tmp_02 
order by user_regdate;




--------------------------------------------------------------------
--------------------------------------------------------------------

---------------------------------------
-- A게임의 아이템별 가장 같이 잘팔리는 아이템찾기
with tmp_01 as (
select a.userkey, a.package_name as prod_01, b.package_name as prod_02 
from purchase as a
join purchase as b
on a.userkey = b.userkey
where a.package_name != b.package_name
and a.game_id = 'A'
),
tmp_02 as (
select prod_01, prod_02, count(*) as cnt
from tmp_01
group by prod_01, prod_02
),
tmp_03 as (
select prod_01, prod_02, cnt, 
row_number() over (partition by prod_01 order by cnt desc) as rnum
from tmp_02
)
select prod_01, prod_02, cnt
from tmp_03
where rnum = 1
order by cnt desc;


--------------------------------
-- A게임의 RFM 분석 (각 카테고리별 A, B, C 등급 분류)
with tmp_01 as (
select p.userkey, max(date_trunc('day', p.logdate_kst))::date as max_ord_date,
to_date('20210201', 'yyyymmdd') - max(date_trunc('day', p.logdate_kst))::date as recency,
count(distinct(p.logtime_kst)) as frequency,
sum(price) as money
from userinfo u
left join purchase p
on u.userkey = p.userkey
where p.game_id = 'A'
group by p.userkey
),
tmp_02 as (
select 'A' as grade, 1 as fr_rec, 18 as to_rec, 7 as fr_freq, 671 as to_freq,  17967800.0 as fr_money, 148024000.0 as to_money
union all
select 'B', 19, 56, 3, 6, 2801000.0, 17464900.0
union all
select 'C', 57, 124, 1, 2, 0.0, 2796000
),
tmp_03 as (
select a.*, b.grade as recency_grade, c.grade as frequency_grade, d.grade as money_grade
from tmp_01 a
left join tmp_02 b on a.recency between b.fr_rec and b.to_rec
left join tmp_02 c on a.frequency between c.fr_freq and c.to_freq
left join tmp_02 d on a.money between d.fr_money and d.to_money
)
select * from tmp_03;


-- B게임의 RFM 분석 (각 카테고리별 A, B, C 등급 분류)
with tmp_01 as (
select p.userkey, max(date_trunc('day', p.logdate_kst))::date as max_ord_date,
to_date('20210201', 'yyyymmdd') - max(date_trunc('day', p.logdate_kst))::date as recency,
count(distinct(p.logtime_kst)) as frequency,
sum(price) as money
from userinfo u
left join purchase p
on u.userkey = p.userkey
where p.game_id = 'B'
group by p.userkey
),
tmp_02 as (
select 'A' as grade, 1 as fr_rec, 37 as to_rec, 6 as fr_freq, 957 as to_freq,  24955100.0 as fr_money, 177168700.0 as to_money
union all
select 'B', 38, 95, 2, 5, 3293000.0, 24827500.0
union all
select 'C', 96, 124, 1, 1.1, 0.0, 3290500.0
),
tmp_03 as (
select a.*, b.grade as recency_grade, c.grade as frequency_grade, d.grade as money_grade
from tmp_01 a
left join tmp_02 b on a.recency between b.fr_rec and b.to_rec
left join tmp_02 c on a.frequency between c.fr_freq and c.to_freq
left join tmp_02 d on a.money between d.fr_money and d.to_money
)
select * from tmp_03;


----------------------------------------------------------------
----------------------------------------------------------------


-- 게임별 국가별 총 매출액 (전체기간)
with tmp_01 as (
select u.game_id, u.userkey as userkey_u, u.geo, u.media, u.os, u.regdate_kst, 
p.userkey as userkey_p, p.logtime_kst, p.market_code, p.package_name, p.price
from userinfo as u
left join purchase as p
on u.userkey = p.userkey
)
select game_id, geo, sum(price) as total_sum
from tmp_01 
group by game_id, geo
order by game_id, total_sum desc;
-- 게임별 국가별 총 매출액 (전체기간)
with tmp_01 as (
select u.game_id, u.userkey as userkey_u, u.geo, u.media, u.os, u.regdate_kst, 
p.userkey as userkey_p, p.logtime_kst, p.market_code, p.package_name, p.price
from userinfo as u
left join purchase as p
on u.userkey = p.userkey
),
tmp_02 as (
select geo as geo_a, sum(price) as total_sum_a
from tmp_01
where game_id = 'A'
group by geo
),
tmp_03 as (
select geo as geo_b, sum(price) as total_sum_b
from tmp_01
where game_id = 'B'
group by geo
)
select *
from tmp_02 as a
join tmp_03 as b
on a.geo_a = b.geo_b;


-- S국가의 게임별 미디어별 총 매출액
with tmp_01 as (
select u.game_id, u.userkey as userkey_u, u.geo, u.media, u.os, u.regdate_kst, 
p.userkey as userkey_p, p.logtime_kst, p.market_code, p.package_name, p.price
from userinfo as u
left join purchase as p
on u.userkey = p.userkey
where geo = 'S'
),
tmp_02 as (
select media as media_a, sum(price) as total_sum_a
from tmp_01
where game_id = 'A'
group by media
),
tmp_03 as (
select media as media_b, sum(price) as total_sum_b
from tmp_01
where game_id = 'B'
group by media
)
select *
from tmp_02 as a
left join tmp_03 as b
on a.media_a = b.media_b;


-- S국가의 게임별 os별 총 매출액
with tmp_01 as (
select u.game_id, u.userkey as userkey_u, u.geo, u.media, u.os, u.regdate_kst, 
p.userkey as userkey_p, p.logtime_kst, p.market_code, p.package_name, p.price
from userinfo as u
left join purchase as p
on u.userkey = p.userkey
where geo = 'S'
),
tmp_02 as (
select os as os_a, sum(price) as total_sum_a
from tmp_01
where game_id = 'A'
group by os
),
tmp_03 as (
select os as os_b, sum(price) as total_sum_b
from tmp_01
where game_id = 'B'
group by os
)
select *
from tmp_02 as a
left join tmp_03 as b
on a.os_a = b.os_b;


-- A게임의 구매자당 평균 매출 (월별 리텐션)
with tmp_01 as (
select userkey, min(logdate_kst) as first_date
from purchase
group by userkey
),
tmp_02 as (
select a.*, b.first_date
from purchase a
left join tmp_01 b
on a.userkey = b.userkey
),
tmp_03 as (
select p.userkey, date_trunc('month', p.first_date)::date as first_date, date_trunc('month', p.logdate_kst)::date as user_logdate, sum(p.price) as total_price
from userinfo u
left join tmp_02 p 
on u.userkey = p.userkey
where p.game_id = 'B'
and u.geo = 'ETC'
and (u.regdate_kst >= '2020-10-01' and u.regdate_kst <= '2021-01-31')
group by p.userkey , date_trunc('month', p.first_date)::date, date_trunc('month', p.logdate_kst)::date
),
tmp_04 as (
select first_date, count(distinct(userkey)) as cnt,
sum(case when user_logdate = first_date then total_price else null end ) as m0_sum,
sum(case when user_logdate = first_date + interval '1 month' then total_price else null end ) as m1_sum,
sum(case when user_logdate = first_date + interval '2 month' then total_price else null end ) as m2_sum,
sum(case when user_logdate = first_date + interval '3 month' then total_price else null end ) as m3_sum
from tmp_03
group by first_date
order by first_date
)
select first_date, cnt,
round(m0_sum/cnt, 0) as m0,
round(m1_sum/cnt, 0) as m1,
round(m2_sum/cnt, 0) as m2,
round(m3_sum/cnt, 0) as m3
from tmp_04 
order by first_date;


-- S국가 A게임의 ARPU (전체기간)
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'B'
and A.geo = 'ETC'
)
select sum(price) as total_sum_a, count(distinct(userkey_a)) as total_user_a,
round( (sum(price) / count(distinct(userkey_a))::numeric), 2) as ARPU_a
from tmp;


-- S국가 A게임의 ARPPU (전체기간)
with tmp as (
select A.game_id, A.userkey as userkey_a, A.geo, A.media, A.os, A.regdate_kst, B.userkey as userkey_b, B.logtime_kst, B.market_code, B.package_name, B.price
from userinfo as A
left join purchase as B
on A.userkey = B.userkey
where A.game_id = 'B'
and A.geo = 'ETC'
)
select sum(price) as total_sum, count(distinct(userkey_b)) as cnt,
round( sum(price)/count(distinct(userkey_b))::numeric , 2) as ARPPU
from tmp
group by game_id;