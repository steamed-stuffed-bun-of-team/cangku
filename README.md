    import java.awt.BorderLayout;
    import java.awt.Container;
    import java.awt.FlowLayout;
    import java.awt.Font;
    import java.awt.GridLayout;
    import java.awt.event.ActionEvent;
    import java.awt.event.ActionListener;
    import java.io.File;
    import java.io.IOException;

    import javax.swing.JButton;
    import javax.swing.JFrame;
    import javax.swing.JLabel;
    import javax.swing.JPanel;
    import javax.swing.JPasswordField;
    import javax.swing.JTextField;

    import jxl.Cell;
    import jxl.Sheet;
    import jxl.Workbook;
    import jxl.read.biff.BiffException;

    public class Ten_login extends JFrame implements ActionListener {
	      JLabel jl1;
        JLabel jl2;
        JLabel jl3;
         JTextField name;	// 定义可编辑的文本框变量
        JPasswordField password;  	// 定义可编辑的密码框变量
        JButton jb;     // 定义按钮变量
       JButton button;     // 定义按钮变量
       static String p3;
       String a="100";
       String b="100";
	 public Ten_login(){
		  //新建窗体
		  Container cp=getContentPane();
		  cp.setLayout(null);
		  //添加用户名标签和用户名输入框
	    jl1=new JLabel("用户名：");
	    //jl1.Font("宋体", Font.BOLD, 32);
		  jl1.setBounds(120, 20, 200, 36);
		
    name=new JTextField();
		name.setBounds(200, 20, 200, 36);
		//添加密码标签和密码输入框
		jl2=new JLabel("密码：");
		jl2.setBounds(120, 100, 200, 36);
		password=new JPasswordField();
		password.setBounds(200, 100, 200, 36);
		//添加显示登录结果的空标签
		jl3=new JLabel("");
		jl3.setBounds(160, 160, 200, 36);
		//把标签和输入框添加到容器
		cp.add(jl1);
		cp.add(name);
		cp.add(jl2);
		cp.add(password);
		cp.add(jl3);
		
		//添加确定按钮，并给按钮加事件
		jb=new JButton("确定");
		jb.addActionListener(new ActionListener(){
			int i=1;

			public void actionPerformed(ActionEvent e) {
			int p1=name.getText().trim().length();  //用户名的长度
            int p2=new String(password.getPassword()).trim().length();//密码的长度
			if(p1==0||p2==0){
				jl3.setText("用户名密码不允许为空");
				return;
			}
			p3=name.getText().trim(); //用户名的值
            String p4=new String(password.getPassword()).trim(); //密码的值
            try {
				Workbook wb = Workbook.getWorkbook(new File("G:\\banks\\bank.xls"));
				Sheet sheet = wb.getSheet(0);
				for(int j=0; sheet.getCell(0, j).getContents().equals("111")!=true; j++){
            		if(p3.equals(a)==true) break;
				Cell cell_user = sheet.getCell(0, j);
				Cell cell_password = sheet.getCell(7, j);
				a = cell_user.getContents();
				b = cell_password.getContents();
				System.out.print(p3+" ");
				System.out.println(a+" "+b + " " +1);
				//i++;
				}
				//System.out.println(a);
				wb.close();
			} catch (BiffException e1) {
				// TODO 自动生成的 catch 块
				e1.printStackTrace();
			} catch (IOException e1) {
				// TODO 自动生成的 catch 块
				e1.printStackTrace();
			}
            if(p3.equals(a)&&p4.equals(b)){ //如果用户名等于mr,密码等于mrsoft 
				jl3.setText("登录成功");
				setVisible(false);
				dispose();
				new Ten_member_two();
			}
			else{
				jl3.setText("用户名或密码错误");
				return;
			}
		}
		});
		
		jb.setBounds(160, 240, 100, 36);
		cp.add(jb);
		
    //添加重置按钮，并给按钮加事件
	    button = new JButton("重置");
		button.addActionListener(new ActionListener(){
			public void actionPerformed(ActionEvent e) {
				name.setText("");   //用户名为空
				password.setText("");//密码为空 
			}
		});
		button.setBounds(300, 240, 100, 36
				);
		cp.add(button);
		    setVisible(true);
			setTitle("超市仓库管理系统");
			setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
			setBounds(600, 400, 600, 400);
	}
    public static void main(String[] args)  {
		new Ten_login();

	}
	@Override
	public void actionPerformed(ActionEvent e) {
		// TODO 自动生成的方法存根
		
	}

}
