删除评估报告310（result_assessment_id）的重复评估（result_id），保留最新的（max）
```SQL
delete from result_assessment where assessment_meta_id=310 and result_assessment_id not in (
	select result_assessment_id 
	from (
		select
			max(result_assessment_id) as result_assessment_id
		from 
			result_assessment 
		where 
			assessment_meta_id=310 
		group by result_id 
	) as xx
)
```
