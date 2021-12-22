### 微擎数据库操作

```php
public function main()

	{
		global $_W;
	//查询
		// $data = '你哈';
		// show_json('data' => $data);
		// $data= pdo_fetchall('SELECT * FROM ' . tablename('ewei_shop_waterpurifier_member_copy') . " WHERE name = :name", array(':name' => '吴鹏'));
		// $data= pdo_fetchall('SELECT * FROM ' . tablename('ewei_shop_waterpurifier_member_copy') . " WHERE id > :id", array(':id' => '2'));

				//获取id大于2的数据
		// $sql = "SELECT * FROM ".tablename('ewei_shop_waterpurifier_member_copy') . " WHERE id > 2 " ;
		// $data = pdo_fetchall($sql);  
		// $data=$data[id];
		
		//获取id大于1的数据
		// $account = pdo_fetchall('SELECT * FROM ' . tablename('ewei_shop_waterpurifier_member_copy'), array('id >' => '1'));

		//获取数据总数
		// $user_total = pdo_fetchcolumn("SELECT COUNT(*) FROM" .tablename('ewei_shop_waterpurifier_member_copy') );


		//获取指定字段name id 1个
		// $user = pdo_get('ewei_shop_waterpurifier_member_copy', array('uniacid' => 1), array('name', 'id'));
 		// show_json(array('user' => $user));

		//  $user = pdo_getal('ewei_shop_waterpurifier_member_copy', array('uniacid' => 1), array('name', 'id'),array(1,5));
		//获取指定字段name id 5个
		// $user = pdo_getall('ewei_shop_waterpurifier_member_copy', array('uniacid' => 1), array() , '' , array('name','id'), array(1,5));
		// $user1 = pdo_getall('ewei_shop_waterpurifier_member_copy', array('uniacid' => 1), array() , '' , 'id DESC' , array(1,10));
 		// show_json(array('user1' => $user1));
		// 更新
			// ewei_shop_waterpurifier_member_copy
			// $user_data = array(
			// 	'name' => '阿海哈哈'
			// );
			// $result = pdo_update('ewei_shop_waterpurifier_member_copy',$user_data,array('id' => 2));
			// if(!empty($result)){
			// 	message('更新成功');
			// }
			
		//删除
		// $result = pdo_delete('ewei_shop_waterpurifier_member_copy', array('id' => '12'));
		// if(!empty($result)){
		// 		message('更新成功');
		// 	}		
		
		//添加 
		// $data=array(
		// 		'uniacid'=>  "1",
		// 		'name'=> "李琨",
		// 		'mobile'=>  "1231515611",
		// 		'openid'=>  "",
		// 		'money'=>  "0.00",
		// 		'enabled'=>  "1",
		// 		'adminenabled'=>  "1",
		// 		'address'=>  "N;",
		// 		'type'=>  "1",
		// 		'install'=> "1",
		// 		'repair'=>  "1"
		// );
		// $result = pdo_insert('ewei_shop_waterpurifier_member_copy' , $data);
		// if(!empty($result)){
		// 	message('添加成功');
		// }
		include $this->template();
	}
```

