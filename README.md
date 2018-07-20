package com.fujifilm.common.util;

import java.text.DecimalFormat;
import java.util.Comparator;
import java.util.Map;

public class CisaIdSort implements Comparator {
	public CisaIdSort(){
		super();
	}
	public boolean equals(Object obj) {
		    return (super.equals(obj));
	}

	// ソート条件を実装
	public int compare(Object obj1, Object obj2) {
		Map.Entry ent1 =(Map.Entry)obj1;
		Map.Entry ent2 =(Map.Entry)obj2;
		String val1 = (String) ent1.getKey();
		String val2 = ((String) ent2.getKey());

		int ret1 = 0;
		int ret2 = 0;

		int val1num = 0;
		int val2num = 0;

		try{
			val1num = Integer.parseInt(val1);
		}catch( Exception e ){
			ret1 = 1;
		}

		try{
			val2num = Integer.parseInt(val2);
		}catch( Exception e ){
			ret2 = 1;
		}

		// 共に数字なら
		if(ret1==0 && ret2 == 0){
			return val1num -val2num;
		}

		// 共に文字なら
		else if(ret1==1 && ret2 == 1){
			return val1.compareTo(val2);
		}

		// 片側が数字でないなら
		else{
			return ret1-ret2;
		}
	}
}
重写Collections.sort（）方法
Collections.sort( sorOrgtMap, new CisaIdSort() );
