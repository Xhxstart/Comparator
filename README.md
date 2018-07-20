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

/**
 * 
 */
package com.test.invoke;

import java.beans.IntrospectionException;
import java.beans.PropertyDescriptor;
import java.lang.reflect.InvocationTargetException;

/**
 * @author kigak-ka
 *
 */
public class ReflectDemo {

	/**
	 * @param args
	 * @throws IntrospectionException 
	 * @throws InvocationTargetException 
	 * @throws IllegalArgumentException 
	 * @throws IllegalAccessException 
	 */
	public static void main(String[] args) throws IntrospectionException, IllegalAccessException, IllegalArgumentException, InvocationTargetException
			 {
		person p = new person();
		p.setId("0");
		String[] names = new String[]{""};
		p.setTestID(names);
		PropertyDescriptor prop = new PropertyDescriptor("testID", person.class);
 
		// 获取getter方法，反射获取id值
		String[] str = (String[])prop.getReadMethod().invoke(p);
 
		// 获取setter方法，反射赋值
		//prop.getWriteMethod().invoke(p, "1");
 
		System.out.println("获取ID值:" + str[0]);
		//System.out.println("赋值ID:" + p.getId());
	}


}


/**
 * 
 */
package com.test.invoke;

/**
 * @author kigak-ka
 *
 */
public class person {

		private String tId;
		
		private String id;
		
		private String[] testID;
	 
		public String getId() {
			return id;
		}
	 
		public void setId(String id) {
			this.id = id;
		}
	 
		public String gettId() {
			return tId;
		}
	 
		public void settId(String tId) {
			this.tId = tId;
		}

		/**
		 * @return testID
		 */
		public String[] getTestID() {
			return testID;
		}

		/**
		 * @param testID セットする testID
		 */
		public void setTestID(String[] testID) {
			this.testID = testID;
		}

}


