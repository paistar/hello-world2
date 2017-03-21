# hello-world2
# -*- coding: cp936 -*-
#判断是否闰年，是返回True
def LeafYear(year):
    if year%100==0:
        if year%400==0:
            return True
        else:
            return False
    else:
        if year%4==0:
            return True
        else:
            return False

#算出某一年第一天星期几，星期日是1，星期一是2，以此类推
def yFirstDay(year):
    SumDay=0
    if year<2017:
        for i in range(year,2017):
            if LeafYear(i)==True:
                SumDay=SumDay+366
            else:
                SumDay=SumDay+365
        n=SumDay%7
        if n==0:
            return 1
        else:
            return 8-n
    else:
        for i in range(2017,year):
            if LeafYear(i)==True:
                SumDay=SumDay+366
            else:
                SumDay=SumDay+365
        n=SumDay%7
        return n+1

#算出某年某月有几天
def DaysInMonth(year,month):
    if month in [1,3,5,7,8,10,12]:
        return 31
    elif month in [4,6,9,11]:
        return 30
    else:
        if LeafYear(year)==True:
            return 29
        else:
            return 28

#算出某年某月第一天星期几
def mFirstDay(year,month):
    n0=yFirstDay(year)
    SumDay=0
    for i in range(1,month):
        SumDay=SumDay+DaysInMonth(year,i)
    return (n0-1+SumDay)%7+1

#具体输出某个月
def monthprint(year,month):
    monthword='JanFebMarAprMayJunJulAugSepOctNovDec'
    print 15*' '+monthword[3*month-3:3*month] #输出月份缩写
    print 'Sun  Mon  Tue  Wed  Thu  Fri  Sat'
    firstday=mFirstDay(year,month)
    total=0
    #total用来计算已经输出的字符数（包括每月第一天的前的空格），每七个换一次行
    for k in range(1,firstday):
        print '    ',
        total=total+1  #先把第一天之前的空格输出
    days=DaysInMonth(year,month)
    for i in range(1,days+1):
        print '%3d '%(i), #输出数字但先别过行
        total=total+1
        if total%7==0:
            print #空print语句表示过行
    if total%7!=0:
        print
        #每月打印完之后若还有空格，也要过个行（total能整除7的话前面已经过行了）

#主程序
year=input('input the year')
for month in range(1,13):
    monthprint(year,month)
m=raw_input('press enter to quit')
