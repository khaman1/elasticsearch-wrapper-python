I am using this wrapper as well. All functions are tested successfully. You should figure out how to use it. To amplify the strength of elasticsearch, a multithreading should be used, as well as using cache to reduce workload. Hope this elasticsearch would be helpful for your project.



result    = 	elasticsearch_base(host='127.0.0.1:9250',index='real_estate', password='123456')\
                .match_phrase(field='city_name',      input='new-york')\
                .match_phrase(field='district_name',  input='manhattan')\
                .match_phrase(field='ad_type', input=[user_choice_array['select-house-type']])\
                .match_phrase(field='address', input=[user_choice_array['select-city']])\
                .match_phrase(field='address', input=[user_choice_array['select-district']])\
                .filter_in_time_range(field='posted_date',last_num_of_days=30)\
                .sort(user_choice_array['sort'])\
				.source('ad_id')\
                .exec(count=ITEMS_PER_PAGE*MAX_PAGE_NUM)
				.json(
                    start=ITEMS_PER_PAGE*(page_num-1),
                    end=ITEMS_PER_PAGE*page_num
                )