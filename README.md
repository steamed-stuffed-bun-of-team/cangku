    import java.awt.BorderLayout;
	import java.awt.Color;
	import java.awt.Dimension;
	import java.awt.FlowLayout;
	import java.awt.Font;
	import java.awt.GridLayout;
	import java.awt.event.ActionEvent;
	import java.awt.event.ActionListener;
	import java.awt.event.MouseEvent;
	import java.awt.event.MouseListener;
	import java.io.File;
	import java.io.IOException;

	import javax.swing.ImageIcon;
	import javax.swing.JButton;
	import javax.swing.JFrame;
	import javax.swing.JLabel;
	import javax.swing.JPanel;
	import javax.swing.JTextArea;
	import javax.swing.JTextField;
	import javax.swing.UIManager;
	import javax.swing.plaf.LayerUI;

	import org.omg.CORBA.TypeCodePackage.Bounds;

	import jxl.Cell;
	import jxl.Sheet;
	import jxl.Workbook;
	import jxl.read.biff.BiffException;
	import jxl.write.Label;
	import jxl.write.WritableSheet;
	import jxl.write.WritableWorkbook;
	import jxl.write.WriteException;
	import jxl.write.biff.RowsExceededException;

 	public class Ten_member_two extends JFrame implements ActionListener, MouseListener{
			JButton button_set, button_cargo, button_person, button_inventory, submitQueryConditionID, messageModification, messageAdd, addMessagesubmit, ModificationMessagebutton, deleteButton;
			JPanel panel1, panel2, panel3, panel, panelnew, panelnewuser, paneladd, panelModification, panelModificationButton, panelModificationMessage;
	JLabel commoditylabelQueryId, labelQueryResult, Modificationlabel;
	JButton[] buttons = new JButton[10];
	JLabel[] labels = new JLabel[10]; 	//增加信息的标签组
	JTextField[] textField = new JTextField[10]; //增加信息的文本组
	JTextField ModificationTextField;
	ImageIcon icon = new ImageIcon("src/beijingtu.jpg");
	JTextField queryConditionID;
	private String searchResult = "";
	int sheets = 0;
	public Ten_member_two(){
		
		/*统一字体*/
		Font f = new Font("楷体",Font.PLAIN,26); 
        UIManager.put("Button.font",f);
        UIManager.put("TextField.font",f);
        UIManager.put("Label.font",f);
        UIManager.put("TextArea.font", f);
        
        JLabel label = new JLabel(icon);
        
        /*容器创建*/
		panel1 = new JPanel();//图片容器
		panel2 = new JPanel();//组件容器 north
		panel3 = new JPanel();  //查询容器 center
		panel = new JPanel();  //底层pan
		panelnew = new JPanel();//信息容器
		paneladd = new JPanel(); //增加信息容器
		panelModification = new JPanel(); //修改信息容器
		panelModificationButton = new JPanel(); //修改信息放按钮容器
		panelModificationMessage = new JPanel(); //修改信息操作容器
		
		panel1.setLayout(new BorderLayout());
		
		//panel3.setBackground(Color.BLUE);
		//panel2.setBackground(Color.BLUE);
		
		/*顶端组件容器设置panel2*/
		//panel2.setLayout(null);
		
	//		button_set = new JButton("设置");
	//		button_set.setBounds(100, 1820, 100, 100);
	//		button_set.addActionListener(this);
		
		button_cargo = new JButton("货物信息");
		button_cargo.setBounds(100, 100, 500, 100);
		button_cargo.addActionListener(this);
		
		button_person = new JButton("人员信息");
		button_person.setBounds(300, 100, 500, 100);
		button_person.addActionListener(this);
		
		button_inventory = new JButton("库存管理");
		button_inventory.setBounds(500, 100, 500, 100);
		button_inventory.addActionListener(this);

		//panel2.add(button_set);
		panel2.add(button_person);
		panel2.add(button_cargo);
		panel2.add(button_inventory);
		//panel2.add(deleteButton);
		
		//panel2.setSize(1920, 100);
		panel2.setOpaque(false);
		
		
		/*查询货物信息面板的组件设置(panel3)*/
		panel3.setLayout(null);
		
		commoditylabelQueryId = new JLabel("请输入编号id：");
		commoditylabelQueryId.setBounds(200, 100, 300, 50);
		
		queryConditionID = new JTextField();
		queryConditionID.setBounds(450, 100, 600, 50);
		
		submitQueryConditionID = new JButton("点击查询");
		submitQueryConditionID.setBounds(1100, 100, 200, 50);
		submitQueryConditionID.addActionListener(this);
		
		messageModification = new JButton("数据修改");
		messageModification.setBounds(1350, 100, 200, 50);
		messageModification.addActionListener(this);
		
		messageAdd = new JButton("数据增加");
		messageAdd.setBounds(1600, 100, 200, 50);
		//messageAdd.setForeground(Color.green);
		messageAdd.addActionListener(this);
		
		deleteButton = new JButton("删除全部数据");
		deleteButton.addActionListener(this);
		//deleteButton.setBounds(1850, 100, 200, 50);
		
		labelQueryResult = new JLabel();
		labelQueryResult.setBounds(200, 150, 1700, 200);
		labelQueryResult.setOpaque(false);
		
		addMessagesubmit = new JButton("信息提交");
		addMessagesubmit.addActionListener(this);
		
		panel3.add(commoditylabelQueryId);
		panel3.add(queryConditionID);
		panel3.add(submitQueryConditionID);
		panel3.add(labelQueryResult);
		panel3.add(messageModification);
		panel3.add(messageAdd);
		//panel3.add(deleteButton);
		//panel3.add(paneladd);
		
		
		panel3.setSize(1920, 1080);
		panel3.setOpaque(false);
		panel3.setVisible(false);
		
		/*查询用户信息面板组件panelnewuser*/
		
		//JF面板设置
		setContentPane(panel);
		panel.add(label);
		label.add(panel1);
		panel1.add(panel2, BorderLayout.NORTH);
		panel1.add(panel3, BorderLayout.CENTER);
		//panel1.add(panelnew, BorderLayout.SOUTH);
		
		panel1.setSize(1920, 1080);
		panel1.setOpaque(false);
		
		/*修改信息组件*/
		

		setVisible(true);
		setTitle("管理员id："+ Ten_login.p3);
		//setLocation(450,  100);
		setSize(1920, 1080);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		
	}
	
	@Override
	public void actionPerformed(ActionEvent e) {
		// TODO 自动生成的方法存根
		panel3.setVisible(true);
		if(e.getSource().equals(button_cargo)){
			sheets = 1;
			paneladd.setVisible(false);
			panelModificationButton.setVisible(false);
			panelModificationMessage.setVisible(false);
			labelQueryResult.setText("已切换到查询商品 请输入查询编号");
		}
		if(e.getSource().equals(button_person)){
			sheets = 0;
			paneladd.setVisible(false);
			panelModificationButton.setVisible(false);
			panelModificationMessage.setVisible(false);
			labelQueryResult.setText("已切换到查询用户 请输入查询编号");
		}
		if(e.getSource().equals(button_inventory)){
			sheets = 2;
			paneladd.setVisible(false);
			panelModificationButton.setVisible(false);
			panelModificationMessage.setVisible(false);
			labelQueryResult.setText("已切换到查询库存清单 请输入查询编号");
		}
		
		if(e.getSource().equals(submitQueryConditionID)){
			panelModificationMessage.setVisible(false);
			panelModificationButton.setVisible(false);
			paneladd.setVisible(false);
			String a = "0";
			searchResult = "";
			int p1=queryConditionID.getText().trim().length();  
			if(p1==0){
				labelQueryResult.setText("请输入您要查询的编号！");
				return;
			}
			try {
				String ConditionID = queryConditionID.getText().trim();
				Workbook wb = Workbook.getWorkbook(new File("G:\\banks\\bank.xls"));
				Sheet sheet = wb.getSheet(sheets);
				loop:for(int i=1; i<sheet.getRows(); i++){
            		if(ConditionID.equals(a)){
            			loo1:for(int j=0; j<sheet.getRow(0).length; j++ ){
            				Cell cell_a = sheet.getCell(j, 0);
            				Cell cell_b = sheet.getCell(j, i-1);
            				
            			if(sheets == 0)
            				searchResult += cell_a.getContents()+ cell_b.getContents()+ "  ";
            			if(sheets == 1)
            				searchResult += cell_a.getContents()+ cell_b.getContents()+ "  ";
            			if(sheets == 2)
            				searchResult += cell_a.getContents()+ cell_b.getContents()+ "  ";
            			if(j==sheet.getRow(0).length-1)
            				break loop;
            		}
            		}
            		if(i==39)
            			searchResult = "未查找到该商品  请重新输入！";
				Cell cell_id = sheet.getCell(0, i);
				a = cell_id.getContents();
				}
				wb.close();
			} catch (BiffException e1) {
				// TODO 自动生成的 catch 块
				//e1.printStackTrace();
				labelQueryResult.setText("未查询到id的信息!");
				return ;
			} catch (IOException e1) {
				// TODO 自动生成的 catch 块
				//e1.printStackTrace();
				labelQueryResult.setText("未查询到id的信息!");
				return ;
			}		
			labelQueryResult.setText(searchResult);
		}
		/*数 据 修 改*/
		if(e.getSource().equals(messageModification)){
			panelModificationButton.setVisible(true);
			paneladd.setVisible(false);
			panelModificationButton.removeAll();
			searchResult = "正在进行修改信息  请选择：";
			labelQueryResult.setText(searchResult);
			//panelModificationButton.repaint();
			//panelModificationButton.removeAll();
			int p1=queryConditionID.getText().trim().length();  
			if(p1==0){
				labelQueryResult.setText("请输入您要修改信息的编号！");
				return;
			}
			 try {
				Workbook wb = Workbook.getWorkbook(new File("G:\\banks\\bank.xls"));
				Sheet sheet = wb.getSheet(sheets);
				for(int j=0; j<sheet.getRow(0).length; j++){
					Cell cell_a = sheet.getCell(j, 0);
					buttons[j] = new JButton(cell_a.getContents());
					buttons[j].addActionListener(this);
					panelModificationButton.add(buttons[j]);
				}	wb.close();
				//panelModification.add(panelModificationButton);
				panelModificationButton.repaint();
				panelModificationButton.setLayout(new FlowLayout(FlowLayout.LEFT));
				panelModificationButton.setBounds(200, 350, 1900, 50);
				panelModificationButton.add(deleteButton);
				panelModificationButton.setOpaque(false);
				panel3.add(panelModificationButton);	
				}catch(Exception ee){
					
					ee.getStackTrace();
				}
		}
		
		if(e.getSource().equals(messageAdd)){
			paneladd.setVisible(true);
			panelModificationMessage.setVisible(false);
			panelModificationButton.setVisible(false);
			searchResult = "正在进行数据的添加  请填写：";
			labelQueryResult.setText(searchResult);
			paneladd.removeAll();
			
			/*构建添加JPanel以及组件*/
			int p1=queryConditionID.getText().trim().length();  
			if(p1==0){
				labelQueryResult.setText("请输入您要增加信息的编号！");
				return;
			}
			try{
			Workbook wb = Workbook.getWorkbook(new File("G:\\banks\\bank.xls"));
			Sheet sheet = wb.getSheet(sheets);
			for(int j=0; j<sheet.getRow(0).length; j++){
				Cell cell_a = sheet.getCell(j, 0);
				labels[j] = new JLabel(cell_a.getContents());
				//System.out.println(cell_a.getContents());
				textField[j] = new JTextField();
				textField[j].setPreferredSize(new Dimension(200, 50));
				paneladd.add(labels[j]);
				//paneladd.add(textField[j]);
				if(j== sheet.getRow(0).length-1&& sheets == 2) break;
				paneladd.add(textField[j]);
			}wb.close();
			paneladd.add(addMessagesubmit);
			paneladd.setLayout(new FlowLayout(FlowLayout.LEFT));
			paneladd.setBounds(200, 350, 1700, 150);
			paneladd.setOpaque(false);
			panel3.add(paneladd);			
			}catch(Exception ee){
				ee.getStackTrace();
			}
	
		}
	
		if(e.getSource().equals(addMessagesubmit)){
			int len = 0;
			try {
				Workbook wb = Workbook.getWorkbook(new File("G:\\banks\\bank.xls"));
				Sheet sheet = wb.getSheet(sheets);
				for(len=0;true;len++){
					Cell cell = sheet.getCell(0, len);
					if(cell.getContents().equals("111"))
					    break;
				}System.out.println(len);
				wb.close();
				//System.out.println(len);
            	}catch(Exception ee){
            		ee.getStackTrace();
            	}
			try{
				String ConditionID = queryConditionID.getText().trim();
				System.out.println(1);
				
				Workbook wb = Workbook.getWorkbook(new File("G:\\banks\\bank.xls"));
				System.out.println(2);
				WritableWorkbook wwb = wb.createWorkbook(new File("G:\\banks\\bank.xls"),wb);
				System.out.println(3);
				WritableSheet sheet = wwb.getSheet(sheets);
				System.out.println(4);
				for(int i=0; i<sheet.getRow(0).length+1; i++){
					String n = textField[i].getText().trim();
					System.out.println(n);
					Label[] label = new Label[50];
					 label[i] = new Label(i , len , n);
					sheet.addCell(label[i]);
					searchResult += "正在存储"+i+" ";
					labelQueryResult.setText(searchResult);
				}	System.out.println(5);
				sheet.addCell(new Label(0, len+1 , "111"));
				wwb.write();
				wwb.close();
				//searchResult = "  ";
				searchResult = "存储成功！  隐藏存储窗口!  请继续接下来操作： ";
				//labelQueryResult.setText(searchResult);
				labelQueryResult.setText(searchResult);
				paneladd.setVisible(false);
			}catch(Exception ee){
				ee.getStackTrace();
			}
		}
		
		/*单项信息修改*/
		for(int i=0 ; i<buttons.length; i++){
			if(e.getSource().equals(buttons[i])){
				searchResult = "已选中修改 ";
				labelQueryResult.setText(searchResult+buttons[i].getText().trim());
				panelModificationMessage.removeAll();
				
				Modificationlabel = new JLabel();
				Modificationlabel.setText(buttons[i].getText().trim());
				Modificationlabel.setBounds(0, 0, 200, 50);
				
				ModificationTextField = new JTextField();
				ModificationTextField.setText("");
				ModificationTextField.setBounds(150, 0, 200, 50);
				
				ModificationMessagebutton = new JButton("确认修改");
				ModificationMessagebutton.setBounds(400, 0, 200, 50);
				ModificationMessagebutton.addActionListener(this);
				
				
				panelModificationMessage = new JPanel();
				panelModificationMessage.add(Modificationlabel);
				panelModificationMessage.add(ModificationTextField);
				panelModificationMessage.add(ModificationMessagebutton);
				panelModificationMessage.setOpaque(false);
				panel3.add(panelModificationMessage);
				panel3.repaint();//刷新出加入的组件			
				panelModificationMessage.setLayout(null);
				panelModificationMessage.setBounds(200, 450, 2200, 50);
				//searchResult = ModificationTextField.getText().trim();
				//labelQueryResult.setText(buttons[i].getText().trim()+"已修改为"+ModificationTextField.getText().trim());
			}
		}
		/*确认修改按钮进行数据修改*/
		if(e.getSource().equals(ModificationMessagebutton)){
			Workbook wb;
			int row = 0;
			int low = 0;
			try {
				wb = Workbook.getWorkbook(new File("G:\\banks\\bank.xls"));
				WritableWorkbook wwb = wb.createWorkbook(new File("G:\\banks\\bank.xls"),wb);
				WritableSheet sheet = wwb.getSheet(sheets);
				//Cell cell = sheet.getCell(arg0, arg1)
				//得到行数
				for(int i=0; sheet.getCell(0, i).getContents().equals("111")!=true; i++){
					System.out.println(sheet.getCell(0, i).getContents());
					if(sheet.getCell(0, i).getContents().equals(queryConditionID.getText().trim())){
						row = i;			
					    break;
					}
				}System.out.println(row);
				//得到列数
				for(int j=0; j<sheet.getRow(0).length; j++){
					if(sheet.getCell(j, 0).getContents().equals(Modificationlabel.getText().trim())){
						low = j; break;}
					System.out.println(sheet.getCell(j, 0).getContents());
					System.out.println(Modificationlabel.getText().trim());
				}System.out.println(low);
				if(row!=0){
					Label label = new Label(low, row, ModificationTextField.getText().trim());
					sheet.addCell(label);
				}
				labelQueryResult.setText(Modificationlabel.getText().trim()+"已修改为"+ModificationTextField.getText().trim());
					wwb.write();
					wwb.close();
				//Label label = new Label(c, r, cont);				
			} catch (BiffException e1) {
				// TODO 自动生成的 catch 块
				e1.printStackTrace();
			} catch (IOException e1) {
				// TODO 自动生成的 catch 块
				e1.printStackTrace();
			} catch (RowsExceededException e1) {
				// TODO 自动生成的 catch 块
				e1.printStackTrace();
			} catch (WriteException e1) {
				// TODO 自动生成的 catch 块
				e1.printStackTrace();
			}
			
		}
		if(e.getSource().equals(deleteButton)){
			//String id = queryConditionID.getText().trim();
			Workbook wb;
			int row = 0;
			try {
				wb = Workbook.getWorkbook(new File("G:\\banks\\bank.xls"));
				WritableWorkbook wwb = wb.createWorkbook(new File("G:\\banks\\bank.xls"),wb);
				WritableSheet sheet = wwb.getSheet(sheets);
				
				for(int i=0; sheet.getCell(0, i).getContents().equals("111")!=true; i++){
					System.out.println(sheet.getCell(0, i).getContents());
					if(sheet.getCell(0, i).getContents().equals(queryConditionID.getText().trim())){
						row = i;			
					    break;
					}
				}System.out.println(row);
				sheet.removeRow(row);
				wwb.write();
				wwb.close();
				System.out.println("删除完成");
			} catch (BiffException e1) {
				// TODO 自动生成的 catch 块
				e1.printStackTrace();
			} catch (IOException e1) {
				// TODO 自动生成的 catch 块
				e1.printStackTrace();
			} catch (WriteException e1) {
				// TODO 自动生成的 catch 块
				e1.printStackTrace();
			}
			searchResult = "删除完成";
			labelQueryResult.setText(searchResult);
		}
	}

	@Override
	public void mouseClicked(MouseEvent e) {
		// TODO 自动生成的方法存根
		
	}

	@Override
	public void mousePressed(MouseEvent e) {
		// TODO 自动生成的方法存根
		
	}

	@Override
	public void mouseReleased(MouseEvent e) {
		// TODO 自动生成的方法存根
		
	}

	@Override
	public void mouseEntered(MouseEvent e) {
		// TODO 自动生成的方法存根
		
	}

	@Override
	public void mouseExited(MouseEvent e) {
		// TODO 自动生成的方法存根
		
	}


}
