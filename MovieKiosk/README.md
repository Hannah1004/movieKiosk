# _๐ฅ Movie Kiosk_ (Team Project)    
***
### Period : August 2021,  2weeks
### Personnel : 6 ๋ช.  
***
## ๐ _Environment_       
> UI
> > Java Swing

> Programming Language
> > Java version 11.0.1

> DataBase
> > Oracle DB version 18c
> > > ์ธ๋ถ ๋ผ์ด๋ธ๋ฌ๋ฆฌ
> > > > ojdbc6.jar/HikariCP.jar/sql.jar
***
### ๐ _ER Diagram_
![erd](https://user-images.githubusercontent.com/84116965/129391140-79714a8c-9b84-44e0-84d0-d9c5f5ad916e.png)
***   
### ๐ _Usecase Diagram_  
   
   ![usecase](https://user-images.githubusercontent.com/84116965/129388756-5ee5683e-bd54-4be5-958f-33405dd59fb1.png)

   
*** 
## ๐ _Important_

- ๋์์ธ ํจํด

  - MVC ํจํด์ ๊ธฐ๋ฐ์ผ๋กํ ํจํค์ง ๊ตฌ์ฑ

![mvc](https://user-images.githubusercontent.com/84116965/129394319-e93b844f-7ddc-4608-b708-b31ccc3b31bb.png)

- Java Swing์ ์์ ์ถ๋ ฅ

  - mp4ํ์ผ์ gif๋ก ๋ณํ ํ ํ๋ฉด์ ์ถ๋ ฅ(https://ezgif.com/video-to-gif)



- Swing์ Timer ํด๋์ค๋ฅผ ์ด์ฉํ ๋์ ์ธ ์ฒ๋ฆฌ

  - ํด๋น ์๊ฐ์ด ์ง๋ ํ ์ด๋ฒคํธ ๋ฐ์
***
## ๐ _Core Trouble shooting_   
```java
public Detail_P2_C(String img_path, String name, String price, String quantity, JFrame frame) {
	      LineBorder lineColor = new LineBorder(new Color(87,149,255));

	      setBackground(new Color(255, 255, 255));
	      setLayout(new BorderLayout());
	      setBorder(lineColor);
	      
	      ChkImg img = new ChkImg(img_path,94,87);
	      
	      add(img,"West");
	      
	      JPanel centerPanel = new JPanel();
	      centerPanel.setBackground(Color.white);
	      centerPanel.setLayout(null);
	      
	      JLabel proName = new JLabel(name);
	      proName.setFont(new Font("Lao MN", Font.BOLD | Font.ITALIC, 15));
	      proName.setForeground(Color.black);
	      proName.setBounds(20, 30, 200, 30);

	      JLabel proPrice = new JLabel(price + "์");
	      proPrice.setBounds(220, 30, 78, 31);
	      
	      JLabel proQuan = new JLabel(quantity + "๊ฐ");
	      proQuan.setBounds(342, 35, 32, 16);
	      
	      JButton deleteBtn = new RoundedButton("Delete");
	      deleteBtn.setBounds(410, 30, 50, 50);
	      deleteBtn.setForeground(new Color(255, 0, 0));
	      deleteBtn.setBackground(new Color(255, 30, 255));
	      
	      centerPanel.add(proName);
	      centerPanel.add(proPrice);
	      centerPanel.add(proQuan);
	      centerPanel.add(deleteBtn);
	     
	      add(centerPanel,"Center");
	      
	      deleteBtn.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				new ProductsBasketsDAO().basketDelete(new ProductsBasket(proName.getText()));
				frame.setVisible(false);
				new DetailFrame();
			}
		});
	   }
```
> __ScrollPane Issue__
> > ์ฅ๋ฐ๊ตฌ๋ ํ๋ชฉ๋ค์ ๊ฐ๊ฐ JPanel๋ก ์ด๋ฃจ์ด์ ธ ์๋ค.<br>   
๊ทธ ํจ๋ ์์๋ ํด๋น ํ๋ชฉ์ ์ด๋ฏธ์ง/์ด๋ฆ/๊ฐ๊ฒฉ/์๋์ด ๋ค์ด๊ฐ๋๋ฐ,<br>    
์ด ๋ Panel์ Layout์ null๋ก ์ง์ ํด์ฃผ์ด์ผ setBounds ํจ์๋ก ์ํ๋ ์์น์ ์ฝ์ํ  ์ ์๋ค.<br>      
ํ์ง๋ง JScrollPane Component์ Layout์ Null๋ก ์ง์ ํ๋ฉด ์ ์ฒด ์ฅ๋ฐ๊ตฌ๋์ ์คํฌ๋กค๊ธฐ๋ฅ์ด ๋ค์ด๊ฐ์ง๋ฅผ ์๋๋ค.<br>      
์ด ๋ถ๋ถ์ ํด๊ฒฐํ๊ธฐ ์ํด์๋, ๊ฐ๊ฐ์ ํ๋ชฉ Panel์ ์์๋ค์ setBounds๋ก ์ํ๋ ์์น์ ๋ฃ์ ํ์<br>      
๊ทธ JPanel์ ๋ค์ JPanel2์ ๋ฃ์ด์ฃผ๊ณ ,JPanel2์ Layout์ Default๊ฐ BorderLayout์ผ๋ก ์ง์ ํ๋ค.<br>      
์ฌ๊ธฐ์ ์ฃผ์ํ ์ ์ Scroll ๊ธฐ๋ฅ์ ์ ์ฌ์ด๋์ ๋์ ์ปดํจํฐ๊ฐ ์ธ์งํด์ผ ๋ค์ด๊ฐ๊ธฐ ๋๋ฌธ์<br>      
JScrollPane์ Component๋ก ๋ค์ด๊ฐ๋ JPanel์์ ์์(JButton,JLabel)์ค ํ๋๋ผ๋ "East","West"์ ์ง์ ์ด ๋์์ด์ผ ํ๋ค<br>

```java
public class ProductList {
  public static void main(String[] args) {
  	
    if(pbDAO.basketList().size() == 0) {
			JPanel noData = new JPanel();
			noData.setBackground(new Color(255,254,230));
			JLabel msg = new JLabel("์ฅ๋ฐ๊ตฌ๋์ ์ํ์ด ์์ต๋๋ค");
			msg.setFont(new Font("Lucida Grande", Font.BOLD, 20));
			noData.add(msg);
			scroll = new JScrollPane(noData);
			add(scroll);
			scroll.setBounds(0, 67, 600, 383);
			scroll.setVisible(true);
		} else {
			
			for(int i = 0; i < pbDAO.basketList().size(); ++i) {
				
				panel2_1.add(new Detail_P2_C(
						pbDAO.basketList().get(i).getImgPath(),
						pbDAO.basketList().get(i).getName(),
						pbDAO.basketList().get(i).getPrice(),
						pbDAO.basketList().get(i).getQuantity(),
						this));
				
				panel2.add(panel2_1.get(i));
				
				prices.add(Integer.parseInt(pbDAO.basketList().get(i).getPrice()));
			}
			scroll = new JScrollPane(panel2);
			add(scroll);
			
			scroll.setBounds(0, 67, 600, 383);
			scroll.setVisible(true);
		}
  }
}
```
## ๐  _Troubles_   
<details>
	<summary>Cancel Seats & Rollback Button</summary>      
	
> Problem
> > ์ข์์ ๊ณ ๋ฅด๋ ๊ณผ์ ์์ ์ข์์ ์ ํํ ํ ๋ง์์ด ๋ฐ๋์ด์ ๊ณจ๋๋ ๊ฒ์ ์ทจ์ํ๊ธฐ ์ํด <br>ํ ๋ฒ ๋ ํด๋ฆญํ๋ฉด ์๋์ ์์ผ๋ก ๋์์์ผ ํ์ผ๋ ๋ฒํผ์ ์๊น์ ๋ฐ์์ค๋ ๋ฉ์๋๋ฅผ ์ฐพ์ง ๋ชปํด ๋งํ์์ต๋๋ค.
> > > Solution 
> > > >๊ฐ ๋ฒํผ์ด ํ์ฌ ์ ํ์ด ๋์๋์ง ์๋์๋์ง ๋ด์๋ ๋ฐฐ์ด์ ์ ์ญ๋ณ์๋ก ๋ง๋ค์ด ๋์ด ์ํ๋ฅผ ํ์ธํ  ์ ์๋ค๋ฉด ๋  ๊ฒ์ด๋ผ๊ณ  ์๊ฐํ์ต๋๋ค<br> ํด๋์ค์ boolean ํ์์ ๋ฐฐ์ด์ ๋ง๋ ๋ค false์ํ์์ ํด๋ฆญ์ ํ์ ๊ฒฝ์ฐ ํด๋น index์ ๊ฐ์ true๋ก ๋ฐ๊ฟ์ฃผ๊ณ  ์๊น์ ๋ฐ๊ฟ์ฃผ์์ผ๋ฉฐ<br> true์์ ๋ค์ ํด๋ฆญ์ ํ์ ๊ฒฝ์ฐ false๋ก ๋ฐ๊พผ ๋ค ์๋์ ์๊น๋ก ๋์ค๊ฒ ๋ง๋ค์์ต๋๋ค.

```java
	if(SeatChoice_1.th1e_btn_selected[index - 1])
         {
            SeatChoice_1.th1e_btn_selected[index - 1] = false;
            btn.setBackground(new Color(0x404040));
            SeatChoice_1.selected_cnt--;
            SeatChoice_1.ticket_price -= SeatChoice_1.th1e_btn_price[index - 1];
            SeatChoice_1.price_label.setText("์ผ๋ฐ: " + (PeopleCheck.adult_cnt + PeopleCheck.child_cnt + PeopleCheck.old_cnt) + "              " + "์ฅ์ ์ธ: " + PeopleCheck.disable_cnt + "              " + "๊ฐ๊ฒฉ: " + SeatChoice_1.ticket_price);

         }
         else
         {
            if(SeatChoice_1.peoples > SeatChoice_1.selected_cnt)
            {
               SeatChoice_1.th1e_btn_selected[index - 1] = true;
               btn.setBackground(new Color(0xFF3333));
               SeatChoice_1.selected_cnt++;
               SeatChoice_1.ticket_price += SeatChoice_1.th1e_btn_price[index - 1];
               SeatChoice_1.price_label.setText("์ผ๋ฐ: " + (PeopleCheck.adult_cnt + PeopleCheck.child_cnt + PeopleCheck.old_cnt) + "              " + "์ฅ์ ์ธ: " + PeopleCheck.disable_cnt + "              " + "๊ฐ๊ฒฉ: " + SeatChoice_1.ticket_price);
            }
	
```

</details> 

<details>
	<summary>Duplicate selection error</summary>
	
> Problem
> > ์ธ์์๋ฅผ ๊ณ ๋ฅด๋ ๊ณผ์ ์์ ์ธ์์๋ฅผ ํด๋ฆญํ ๋ค ๋ง์์ด ๋ฐ๋์ด ๋ค๋ฅธ ์ํ๋ฅผ ์ ํํ์ ๋ <br>์ธ์์๋ฅผ ๊ณ ๋ฅด๋ ํ๋ ์์ ๊ธฐ์กด์ ํด๋ฆญ๋ผ์๋ ๋ฒํผ์ด ๊ทธ๋๋ก ํด๋ฆญ๋์ด์๋ ๋ฌธ์ ๋ฅผ ๊ฒช์์์ต๋๋ค
> > > Solution 
> > > > ๋งค๋ฒ ์ธ์์๋ฅผ ๊ณ ๋ฅด๋ ํ๋ ์์ด ๋ด์๋ ๋ง๋ค ๋ฒํผ๋ค์ ์ด๊ธฐํํด์ค๋ค๋ฉด ํด๊ฒฐ์ด ๋  ๊ฒ์ด๋ผ๊ณ  ์๊ฐํ์ต๋๋ค<br>์ธ์์๋ฅผ ๊ณ ๋ฅด๋ค๊ฐ ๋๋ ์ข์์ ๊ณ ๋ฅด๋ค๊ฐ ๋ค๋ฅธ ์ํ๋ฅผ ๋ณด๊ณ  ์ถ์ด์ง ๊ฒฝ์ฐ ์ด์ ์ผ๋ก ๋์๊ฐ๋ ํญ์ 0๋ช์ ๋ฒํผ์ด ์ฒดํฌ๋ผ์๋๋ก ๋ง๋ค์์ต๋๋ค

```java
for(int i = 1; i < btns1.size(); i++) {
				adult_btn.get(i).setBackground(new Color(0x404040));
				child_btn.get(i).setBackground(new Color(0x404040));
				disable_btn.get(i).setBackground(new Color(0x404040));
				old_btn.get(i).setBackground(new Color(0x404040));
			}
			adult_cnt = 0;
			child_cnt = 0;
			disable_cnt = 0;
			old_cnt = 0;
			pre_adult_btn_num = 0;
			now_adult_btn_num = 0;
			pre_child_btn_num = 0;
			now_child_btn_num = 0;
			pre_disable_btn_num = 0;
			now_disable_btn_num = 0;
			pre_old_btn_num = 0;
			now_old_btn_num = 0;

		adult_btn.get(0).setBackground(new Color(0xCC0066));
		child_btn.get(0).setBackground(new Color(0xCC0066));
		disable_btn.get(0).setBackground(new Color(0xCC0066));
		old_btn.get(0).setBackground(new Color(0xCC0066));
	
```

</details>
	
<details>
	<summary>Check Type Verification</summary>   
	
> Problem
> > ์ข์ ์ ํ์ค ์ฅ์ ์ธ์์ ์ซ์๋ ํ์ ์ ์ธ๋ฐ ์ฅ์ ์ธ์ด ์๋ ์ฌ๋์ด ์ฅ์ ์ธ์์ ์์ฝํ๋ ๊ฒฝ์ฐ ์ค๋ฅ ๋ฉ์์ง๋ฅผ ๋์์ผ ๋๋ค๊ณ  ์๊ฐํ์ผ๋<br> ์ฌ๋ ์ธ์ ์ค์์ ์ฅ์ ์ธ์ ์ซ์๋ฅผ ์ ์๊ฐ ์์ด์ ๋ฌธ์ ์์ต๋๋ค
> > > Solution 
> > > > ์ธ์์๋ฅผ ์ ์ฒด์ธ์์ด ์๋ ์ฅ์ ์ธ ์ธ์์ ๋ณ์์ ๋ฐ๋ก ์ ์ฅํด๋์ด ์ธ์ ์๋ฅผ ํ์ธํ๋ฉด ๋  ๊ฒ์ด๋ผ๊ณ  ์๊ฐํ์ต๋๋ค<br>์ฅ์ ์ธ ์ธ์์๋ณด๋ค ๋ง์ ์๋ฅผ ์์ฝํ๋ ค๊ณ  ํ๋ฉด ์๋ฌ ๋ฉ์์ง๋ฅผ ๋์ค๊ฒ ์ค์ ํด๋์ด์ ์ฅ์ ์ธ์์ ์ฅ์ ์ธ๋ง ์์ฝํ  ์ ์๊ฒ ํ์ต๋๋ค

```java
if(PeopleCheck.disable_cnt == 0)
                  {
                     ErrorFrame frame = new ErrorFrame();
                     frame.getContentPane().setBackground(new Color(0x404040));
                     frame.setDefaultOptions();
                     JLabel label = new JLabel();
                     label.setText("์ฅ์ ์ธ๋ง ์์ฝ ๊ฐ๋ฅํฉ๋๋ค.");
                     label.setFont(new Font("๋์", Font.PLAIN|Font.BOLD, 30));
                     label.setForeground(Color.white);
                     label.setHorizontalAlignment(JLabel.CENTER);
                     frame.add(label);
                  }
                  else
                  {
                     if(PeopleCheck.disable_cnt > SeatChoice_1.disable_btn_cnt)
                     {
                        SeatChoice_1.th1a_btn_selected[index - 1] = true;
                        btn.setBackground(new Color(0xFF3333));
                        SeatChoice_1.disable_btn_cnt++;
                        SeatChoice_1.selected_cnt++;
                        SeatChoice_1.ticket_price += SeatChoice_1.th1a_btn_price[index - 1];
                        SeatChoice_1.price_label.setText("์ผ๋ฐ: " + (PeopleCheck.adult_cnt + PeopleCheck.child_cnt + PeopleCheck.old_cnt) + "              " + "์ฅ์ ์ธ: " + PeopleCheck.disable_cnt + "              " + "๊ฐ๊ฒฉ: " + SeatChoice_1.ticket_price);
                     }
                     else
                     {
                        ErrorFrame frame = new ErrorFrame();
                        frame.getContentPane().setBackground(new Color(0x404040));
                        frame.setDefaultOptions();
                        JLabel label = new JLabel();
                        label.setText("์ฅ์ ์ธ๋ง ์์ฝ ๊ฐ๋ฅํฉ๋๋ค.");
                        label.setFont(new Font("๋์", Font.PLAIN|Font.BOLD, 30));
                        label.setForeground(Color.white);
                        label.setHorizontalAlignment(JLabel.CENTER);
                        frame.add(label);
                     }
	
```

</details>

<details>
	<summary>Exception in thread "AWT-EventQueue-0" java.lang.NumberFormatException: null</summary>    
	
> Problem
> > ์์ฑ์์์ date(์ผ๋ณ ๋ ์ง) ๊ฐ์ ๋ฐ์์จ ํ ๋ฌ๋ ฅ์์ ๋ ์ง์ ์ซ์๊ฐ ํ ์๋ฆฌ์ผ ๋ ์์ "0"์ด ๋ถ์ฌ์ง ์ ์๋๋ก ์์ฑํด๋์
 getSales() ํจ์์์ date๊ฐ์ ์ฌ์ฉํด์ผ ํ๋๋ฐ, ์์ฑ์์ ์ ์ธํ date ์ด์ ์ getSales() ํจ์๋ฅผ ๋ถ๋ฌ์๊ธฐ ๋๋ฌธ์ null๊ฐ์ด ๋์จ๋ค.
> > > Solution 
> > > > this.date = date; ๋ฐ์ getSales();๋ฅผ ์๋ ฅํด์ฃผ์ด์ผ ์ค๋ฅ๊ฐ ํด๊ฒฐ์ด ๋๋ค.

```java
public S2Panel3(String date) {
		this.date = date;
		getSales();
		setBackground(Color.CYAN);
		setBounds(12, 229, 362, 134);
		setLayout(null);
		l1 = new JLabel("์ ํ");
		l2 = new JLabel("์๋ : " + count);
		l3 = new JLabel("๊ฐ๊ฒฉ : " + sales);
		
		l1.setFont(new Font("๊ตด๋ฆผ", Font.PLAIN, 50));
		l1.setHorizontalAlignment(SwingConstants.CENTER);
		l1.setBounds(12, 10, 140, 114);
		
		l2.setFont(new Font("๊ตด๋ฆผ", Font.PLAIN, 20));
		l2.setBounds(164, 10, 200, 50);
		
		l3.setFont(new Font("๊ตด๋ฆผ", Font.PLAIN, 20));
		l3.setBounds(164, 70, 200, 50);
		
		add(l1);
		add(l2);
		add(l3);
	}
	
```

</details>
	
<details>
	<summary>Design Size Error</summary>

- ์ํ๋ค์ ํ์๋ณ๋ก ๋๋ ์ ๋ฒํผ์ผ๋ก ๋ง๋ค์ด์ฃผ๋ ๋ฉ์๋๋ค์ด๋ค.
- ์ฒ์์๋ ๋ฒํผ์ ์ด๋ฏธ์ง์ ๊ธ(๊ฐ๊ฒฉ, ์ด๋ฆ)๋ก ๋๊ฐ๋ก๋ง ๋ฉ์๋๋ฅผ ๋๋ ์ ํ์๋ค.
- ๋๊ฐ๋ก๋ง ํ์๋๋ ์ด๋ฏธ์ง์ ์ฌ์ด์ฆ๋ฅผ ์ค์ด๋๋ฐ ์ ๊ฐ๊ฐ์ผ๋ก ๋ฐ๊ปด์ ๋์์ธ์ ์ค๋ฅ๊ฐ ์๊ฒผ๋ค.
- ๋ํ ๋ฒํผ์ ๊ธ ์์ฑํ๋ ๋ฐฉ๋ฒ์ด JLabel์ด ์์๋๋ฐ JLabel๋ก ์ฌ๋ฌ๊ฐ ๋๋ ์ ํ๋๊ฒ๋ณด๋ค <br>html๋ก ํ๋ ๋ฐฉ๋ฒ์ด ํจ์จ์ ์ด๋ผ ์๊ฐํด์ html๋ก ๋ง๋ค์ด์ฃผ๋ ๋ฉ์๋๋ฅผ ๋ง๋ค์๋ค.
   
```java
/**
	products๋ค์ ์ด๋ฆ๊ณผ ๊ฐ๊ฒฉ๋ฅผ gui์ ๋ณด์ฌ์ฃผ๊ธฐ์ํด html๋ฅผ ํ์ฉํด text๋ฅผ ๋ง๋ค์๋ค.
	@param name : ์ ํ๋ค ์ด๋ฆ
	@param price : ์ ํ๋ค ๊ฐ๊ฒฉ
	@return : ArrayList<String>
 */
public ArrayList<String> p_text(ArrayList<String> name, ArrayList<Integer> price) {
	ArrayList<String> result = new ArrayList<>();
	
    for (int i = 0; i < name.size(); ++i) {
		DecimalFormat formatter = new DecimalFormat("###,###");	
		result.add("<HTML>" + name.get(i) + "<br>" + formatter.format(price.get(i)) + "์</HTML>");
	}
	return result;
}
	
/**
	ImageIcon ArrayList์ img_path์ ์ฌ์ง์ ๋ฃ์ด์ค๋ค.
	img์ฌ์ด์ฆ๋ ์ค์ด์ค
	@param image_paths : ์ฌ๋ฌ ์ด๋ฏธ์ง path๋ค์ด ๋ค์ด๊ฐ ์์
	@return ArrayList<ImageIcon>
*/
public ArrayList<ImageIcon> makeImageIconArray(ArrayList<String> image_paths) {
	ArrayList<ImageIcon> icons = new ArrayList<>();
    
	for (String path : image_paths) {
		ImageIcon originIcon = new ImageIcon(path);
		Image resizeIcon = originIcon.getImage().getScaledInstance(150, 150, Image.SCALE_SMOOTH);
		
		icons.add(new ImageIcon(resizeIcon));
	}
	return icons;
}

/**
	img์ ์์์ ๋ง๋  name, price์๋ text๋ฅผ ๊ฐ์ง๊ณ  ์ฌ๋ฌ๊ฐ์ ๋ฒํผ ๋ง๋ค๊ธฐ
	@param icons : ๊ฐ๊ฐ์ ์ ํ img๋ค์ด ๋ค์ด์๋ค.
	@param texts : ๊ฐ๊ฐ์ ์ ํ name, price๋ค์ด ๋ค์ด์๋ค.
	@return ArrayList<JButton>
*/
public ArrayList<JButton> btn_list(ArrayList<ImageIcon> icons, ArrayList<String> texts){
	ArrayList<JButton> btns = new ArrayList<>();
	
	for (int i = 0; i < icons.size(); ++i) {
		btns.add(new JButton(texts.get(i),icons.get(i)));
		btns.get(i).setBackground(Color.white);
	}
	return btns;
}

/**
 	ํ์์ ๋ง๋ products๋ค์ ์ ๋ณด ๊ฐ์ ธ์์ ArrayList์ ๋ด์์ฃผ๊ธฐ
 	@param products ArrayList์ ์ ํ ์ ๋ณด ๋ด๊ธฐ
	@param typeName ์ ํ๋ ์ํ type
	@return ArrayList<Products>
*/
public ArrayList<Products> typeOfproduct(ArrayList<Products> products, String typeName){
	ArrayList<Products> array = new ArrayList<>();

	for (int i = 0; i < products.size(); ++i) {
		if (products.get(i).getType().equals(typeName)) {
			array.add(products.get(i));
		}
	}
	return array;
}
```

</details>
	
<details>
	<summary>Get movie information</summary>

> Problem
> > ์ํ ์๊ฐ์ ์ ํํ๋ฉด ๊ทธ์ ๋ฐ๋ฅธ ์ํ ์ ๋ณด์ ๋ค๋ฅธ ์ ๋ณด๋ค์ด ๊ฐ์ด ์์ผ ํ๋ ์ํฉ์ด ์์๋๋ฐ<br>
๋ฒํผ์์ ๊ฐ์ ธ์ฌ ์ ์๋๊ฒ์ ์ํ๊ฐ ์์ํ๋ ์๊ฐ ํ๋๋ผ์ ์ด๊ฒ์ผ๋ก ๋ค๋ฅธ ์ ๋ณด๋ค์ ์ฐ๊ฒฐํด์ ์ฐพ๊ธฐ๊ฐ ์ด๋ ค์ ๋ค<br> 
๋ง์ฝ ๊ฐ์ ์๊ฐ๋์ ์์ํ๋ ๋ค๋ฅธ ์ํ๋ค์ด ์กด์ฌํ๋ฉด ์ด๋ค ์ํ์ ์๊ฐ์ธ์ง ์ ์ ์๊ธฐ์ ์ํ๋ ์ ๋ณด๋ฅผ ์ป์ ์ ์์๋ค<br>
> > > Solution 
> > > > ๋ฒํผ์ ๋ง๋ค ๋ ์ํ๋ง๋ค ์ํ ์ ๋ณด๊ฐ ๋ด๊ฒจ์๋ ํด๋์ค๋ฅผ ๋ฐ๋ก ๋ง๋ค์ด์ <br>
๋ฒํผ์ ๋ฆฌ์ค๋ ๊ธฐ๋ฅ์ ์ถ๊ฐํ  ๋ ๊ทธ์ ๋ง๋ ์ํ ํด๋์ค ์ ๋ณด๋ฅผ ๋ด์ ๋๋ ๋ฐฉ๋ฒ์ ์ ํํ๋ค<br>
1๋ฒ ์ํ๋ฅผ ์ ํํ๋ฉด ๋ฒํผ์ด ๊ตฌํ๋์ด ์๋ ํด๋์ค ์์ฒด์ 1๋ฒ ์ํ์ ์ ๋ณด๋ฅผ ๋ด์ ๋๊ณ 
์๊ฐ ์ ๋ณด๋ ๋ฒํผ์ ์ด๋ฆ์ ์ค์ ํด๋์ ๋ค์<br>
๋ฒํผ์ ํด๋ฆญํ๋ฉด 1๋ฒ ์ํ๊ฐ ๋ด๊ฒจ์ ธ ์๋ ํด๋์ค๋ก ๋์ด๊ฐ๊ณ <br>
ํด๋์ค์๋ ์ด๋ฏธ ๋ฐ์ดํฐ๋ฒ ์ด์ค์์ ๊ฐ์ ธ์จ ์๊ฐ ์ ๋ณด์ ์ํ ์ ๋ณด๋ค์ด ๋ด๊ฒจ ์๊ธฐ์<br>
์๊ฐ๋๋ฅผ ๋น๊ตํด์ ํด๋น ์ํ๊ฐ ๊ฐ์ง๊ณ  ์๋ ๋ค๋ฅธ ์ ๋ณด๋ค์ ๊ฐ์ ธ์ค๋ ๋ฐฉ์์ ์ฌ์ฉํ๋ค<br>
   
```java

	
```

</details>

***  

## ๐ _Bragging Code_    

> `์ํ๊ด ์ข์ํ`
> > ๊ฐ๋จ์ค๋ช   
```java
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("์๋ํ๊ณ  ์ถ์ ์ฝ๋");
  }
}
```   
 
*** 

## ๐ _Video Solution_
- Java Swing ๋์์ ์ถ๋ ฅ

  - javaFx ์ธ๋ถ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ํตํ ๋์์ ์ถ๋ ฅ
  
  ![์ค๋ฅ](https://user-images.githubusercontent.com/84116965/129397173-add4f35f-7aec-4145-b7d3-75567cd09e58.png)
 
  - java 11.0.1๋ฒ์ ์ ํด๋น ์ธ๋ถ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ ์ฐ๋๋ฌธ์ ๊ฐ ์๊น -> GIFํ์ผ๋ก ๋์ฒดํ์ฌ ์ฌ์	
	
*** 

## ๐ธ _Demonstration Video_   
<details>
<summary>GUI ํ๋ฉด ์์</summary>
<div markdown="1">

์์์ฝ์  


</div>
</details>   





