### Spring框架学习（二）
   Spring注入方式有三种：set方法注入、构造方法则注、接口注入。以下主要介绍前两种。

##### 1.set方法注入

  - 给普通字符类型赋值
  
		public class User{
	
			private String username;
			public String getUsername() {
				return username;
			}
			public void setUsername(String username) {
				this.username= username;
			}
		}

	applicationContext.xml
	
    	<bean id="userAction"class="com.lsz.spring.action.User" >
        	<property name="username" value="admin"></property>
    	</bean>

  - 给对象赋值

		public class User{
	
			private UserService userservice;
			public UserService getUserservice() {
				return user;
			}
			public void setUserservice(UserService userservice){
				this.userservice= userservice;
			}
    		}
	配置文件增加对象的声明
	
	<!--对象的声明-->
		
		<bean id="userService" class="com.lsz.spring.service.UserService"></bean>
		<bean id="userAction"class="com.lsz.spring.action.User" >
   			<property name="userservice" ref="userService"></property>
		</bean>

  - 给list集合赋值

		public class User{
	
			private List<String> username;
			public List<String> getUsername() {
				return username;
			}
			public void setUsername(List<String> username) {
				this.username= username;
			}
    		}

	配置文件
		
		<bean id="userAction"class="com.lsz.spring.action.User" >
			<propertynamepropertyname="username">
				<list>
					<value>zhang,san</value>
					<value>lisi</value>
					<value>wangwu</value>
				</list>
			</property>
		</bean>


 - 给属性文件中的字段赋值

		public class User{
        
			private Properties props ;
			public Properties getProps() {
				return props;
			}
			public void setProps(Properties props) {
				this.props= props;
			}
		}

	配置文件
		
		<bean>
			<propertynamepropertyname="props">
				<props>
					<propkeypropkey="url">
						jdbc:oracle:thin:@localhost:orl
					</prop>
					<propkeypropkey="driverName">
						oracle.jdbc.driver.OracleDriver
					</prop>
					<propkeypropkey="username">scott</prop>
					<propkeypropkey="password">tiger</prop>
				</props>
			</property>
		</bean>

 - 注意:无论给什么赋值，配置文件中property标签的name属性值一定是和对象中名称一致

##### 2.构造方法注入

 - 构造方法一个参数
	
		public class User{
        	
			private String usercode;
			public User(String usercode) {
				this.usercode=usercode;
			}
		}
	配置文件
	
		<bean id="userAction"class="com.lsz.spring.action.User">
			<constructor-arg valueconstructor-argvalue="admin">
			</constructor-arg>
		</bean>
 - 构造方法两个参数
	当参数为非字符串类型时，在配置文件中需要制定类型，如果不指定类型一律按照字符串类型赋值。
	当参数类型不一致时，框架是按照字符串的类型进行查找的，因此需要在配置文件中制定是参数的位置
	
		<constructor-arg valueconstructor-argvalue="admin" index="0">
		</constructor-arg>
		<constructor-arg valueconstructor-argvalue="23" type="int" index="1">
		</constructor-arg>
