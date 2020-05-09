我修改cJSON 功能

1.修改了 struct cJSON{} 结构体
    增加了 int valuepoints; 属性        --》 目的 有些地方需要控制小数点位数

2.修改了 cJSON_CreateNumber() 函数 
    cJSON_CreateNumber() 修改内容item->valuepoints=6; 默认小数点个数为 6位

3.增加了 cJSON_CreateNumberWithPoints() 函数
    cJSON *cJSON_CreateNumberWithPoints(double num, int points)			{cJSON *item=cJSON_New_Item();if(item){item->type=cJSON_Number;item->valuedouble=num;item->valueint=(int)num;item->valuepoints=points;}return item;}

4.修改了 print_number() 函数
    修改内容 当valuepoints 为0时 打印整数，否则打印对应的小数点个数的小数
    else												{if(item->valuepoints)sprintf(str,"%.*f",item->valuepoints,d);else sprintf(str,"%d",item->valueint);}


4.增加了 添加基础item(null, bool, number, string) 到数组
#define cJSON_AddNullToArray(object,name)		cJSON_AddItemToArray(object, cJSON_CreateNull())
#define cJSON_AddTrueToArray(object,name)		cJSON_AddItemToArray(object, cJSON_CreateTrue())
#define cJSON_AddFalseToArray(object,name)		cJSON_AddItemToArray(object, cJSON_CreateFalse())
#define cJSON_AddBoolToArray(object,name,b)	cJSON_AddItemToArray(object, cJSON_CreateBool(b))
#define cJSON_AddNumberToArray(object,name,n)	cJSON_AddItemToArray(object, cJSON_CreateNumber(n))
#define cJSON_AddNumberWithPointsToArray(object,name,n,points)	cJSON_AddItemToArray(object, cJSON_CreateNumberWithPoints(n,points))
#define cJSON_AddStringToArray(object,name,s)	cJSON_AddItemToArray(object, cJSON_CreateString(s))