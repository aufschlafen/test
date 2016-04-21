# test
#推箱子
package cn.ui;


import java.awt.Label;
import java.awt.Toolkit;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

import javax.swing.Icon;
import javax.swing.ImageIcon;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.tools.Tool;

import cn.util.common;

public class GameMainFrame extends JFrame implements KeyListener
{
	public GameMainFrame() {
		super.setTitle("推箱子");
		super.setSize(1000,625);
		super.setLocation((Toolkit.getDefaultToolkit().getScreenSize().width-1000)/2, 
				(Toolkit.getDefaultToolkit().getScreenSize().height-625)/2);
		super.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		super.setLayout(null);
		super.setResizable(false);
		person();
		WallLoad();
		
		addKeyListener(this);
		
		super.setVisible(true);
	}
	
	JLabel loadPerson;
	common common=new common();
void person()
	{
		Icon img=new ImageIcon("resource/person.png");
		loadPerson=new JLabel(img);
		loadPerson.setBounds(100,100,50,50);
		super.add(loadPerson);
	}
JLabel loadMap;
	void WallLoad()
	{
		Icon imgWall=new ImageIcon("resource/wall.png");
		Icon imgBox=new ImageIcon("resource/box.png");
		Icon imgTarget=new ImageIcon("resource/endPoint.png");
		JLabel 	loadMap=null;
		for(int col=0;col<cn.util.common.mapData.length;col++)
		{
			for(int row=0;row<cn.util.common.mapData[col].length;row++)
			{
				if(cn.util.common.mapData[col][row]==8){
					
					loadMap=new JLabel(imgWall);
					loadMap.setBounds(row*50,col*50,50,50);
					super.add(loadMap);
				}
				if(cn.util.common.mapData[col][row]==2){
					
					common.lblBoxs[col][row]=new JLabel(imgBox);
					common.lblBoxs[col][row].setBounds(row*50,col*50,  50, 50);
					super.add(common.lblBoxs[col][row]);
				}
				if(cn.util.common.mapData[col][row]==4){
					
					loadMap=new JLabel(imgTarget);
					loadMap.setBounds(row*50,col*50,50,50);
					super.add(loadMap);
			}
			
			}
		}
		
	}

	@Override
	public void keyTyped(KeyEvent e) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void keyPressed(KeyEvent e) {
		int x=0,y=0;
		String dirImg="";
		int input=e.getKeyCode();
		
		switch (input) {
		case 37://左
			dirImg="resource/person_left.png";
			if(cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-1]==8
					||(cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-1]==2&&cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-2]==8)
					||(cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-1]==2&&cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-2]==2))
			{break;}
			if(cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-1]==2)
			{common.lblBoxs[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-1].setLocation((loadPerson.getLocation().x/50-2)*50,loadPerson.getLocation().y);
			common.lblBoxs[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-2]=common.lblBoxs[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-1];
			common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-1]-=2;common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-2]+=2;}
			if(common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-1]==2&&common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-2]==4){
				common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-2]-=2;
				common.lblBoxs[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-1].setLocation((loadPerson.getLocation().x/50-2)*50,loadPerson.getLocation().y);
				common.lblBoxs[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-2]=common.lblBoxs[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50-1];
			}
			x=-50;
			break;
		case 38://上
			dirImg="resource/person_up.png";
			if(cn.util.common.mapData[loadPerson.getLocation().y/50-1][loadPerson.getLocation().x/50]==8
					||(cn.util.common.mapData[loadPerson.getLocation().y/50-1][loadPerson.getLocation().x/50]==2&&cn.util.common.mapData[loadPerson.getLocation().y/50-2][loadPerson.getLocation().x/50]==8)
					||(cn.util.common.mapData[loadPerson.getLocation().y/50-1][loadPerson.getLocation().x/50]==2&&cn.util.common.mapData[loadPerson.getLocation().y/50-2][loadPerson.getLocation().x/50]==2))
			{break;}
			
			if(common.mapData[loadPerson.getLocation().y/50-1][loadPerson.getLocation().x/50]==2){
				common.lblBoxs[loadPerson.getLocation().y/50-1][loadPerson.getLocation().x/50].setLocation(loadPerson.getLocation().x,(loadPerson.getLocation().y/50-2)*50);
				common.lblBoxs[loadPerson.getLocation().y/50-2][loadPerson.getLocation().x/50]=common.lblBoxs[loadPerson.getLocation().y/50-1][loadPerson.getLocation().x/50];
				common.mapData[loadPerson.getLocation().y/50-1][loadPerson.getLocation().x/50]-=2;common.mapData[loadPerson.getLocation().y/50-2][loadPerson.getLocation().x/50]+=2;
			}
			y=-50;
			break;
		case 39://右
			dirImg="resource/person_right.png";
			if(cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+1]==8
					||(cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+1]==2&&cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+2]==8)
					||(cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+1]==2&&cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+2]==2))
			{break;}
			if(cn.util.common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+1]==2)
			{common.lblBoxs[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+1].setLocation((loadPerson.getLocation().x/50+2)*50,loadPerson.getLocation().y);
			common.lblBoxs[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+2]=common.lblBoxs[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+1];
			common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+1]-=2;common.mapData[loadPerson.getLocation().y/50][loadPerson.getLocation().x/50+2]+=2;}
			x=50;
			break;
		case 40://下
			dirImg="resource/person.png";
			if(cn.util.common.mapData[loadPerson.getLocation().y/50+1][loadPerson.getLocation().x/50]==8
					||(cn.util.common.mapData[loadPerson.getLocation().y/50+1][loadPerson.getLocation().x/50]==2&&cn.util.common.mapData[loadPerson.getLocation().y/50+2][loadPerson.getLocation().x/50]==8)
					||(cn.util.common.mapData[loadPerson.getLocation().y/50+1][loadPerson.getLocation().x/50]==2&&cn.util.common.mapData[loadPerson.getLocation().y/50+2][loadPerson.getLocation().x/50]==2))
			{break;}
			if(common.mapData[loadPerson.getLocation().y/50+1][loadPerson.getLocation().x/50]==2){
				common.lblBoxs[loadPerson.getLocation().y/50+1][loadPerson.getLocation().x/50].setLocation(loadPerson.getLocation().x,(loadPerson.getLocation().y/50+2)*50);
				common.lblBoxs[loadPerson.getLocation().y/50+2][loadPerson.getLocation().x/50]=common.lblBoxs[loadPerson.getLocation().y/50+1][loadPerson.getLocation().x/50];
				common.mapData[loadPerson.getLocation().y/50+1][loadPerson.getLocation().x/50]-=2;common.mapData[loadPerson.getLocation().y/50+2][loadPerson.getLocation().x/50]+=2;
			}
			y=50;
			break;
		default:
			break;
			
				
			
		}
		Icon img=new ImageIcon(dirImg);
//		loadPerson=new JLabel(img);
		loadPerson.setIcon(img);
		loadPerson.setLocation(loadPerson.getLocation().x+x,loadPerson.getLocation().y+ y);
		
		
	}
	

	@Override
	public void keyReleased(KeyEvent e) {
		// TODO Auto-generated method stub
		
	}
}
