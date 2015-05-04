---
layout: post
title: Xcode v6.3 - Swift - 第一行代码
category: 'iPhone'
---

##0,Xcode版本号:v6.3

<img src="/images/Xcode-V6.3.png">

##1,创建项目

###(1) 打开Xcode

<img src="/images/1.png">

###(2) 选择项目模板 - Choose a template for your new project

IOS -> Application -> Single View Application

<img src="/images/2.png">

###(3) 项目选项 - Choose options for your new project

Language: Swift

Devices: iPhone

<img src="/images/3.png">

###(4) 保存项目,同时创建git库

<img src="/images/4.png">

###(5) 项目概览

<img src="/images/5.png">

##2,界面设计 - Interface build

###(1) 打开Main.storyboard

<img src="/images/a1.png">

###(2) Embeded In Navigation Controller

Editor -> Embede In -> Navigation Controller

<img src="/images/a2.png">

<img src="/images/a3.png">

###(3) Add New ViewController

点击Main.storyboard,从右下角的object library中选取View Controller对象并拖进界面上,以创建新的ViewController;

从第一个ViewController拉一条线到第二个ViewController,创建一个Segue,动作为show,并命名为"showView";

<img src="/images/a4.png">

<img src="/images/a5.png">

###(4) Add Table View to ViewController

选择设计界面中的第一个ViewController,从右下角的object library中选取Table View对象并拖进界面上,启中放置;

在右上角的attributes inspector中,设置table view的prototype cells为1;

在下方靠右工具栏中选择Resolve Auto Layout Issue -> Add Missing Contraints;

点击左侧面板View Controller Scene -> View Controller -> View -> Table View -> Table View Cell, 在右侧面板Attributes Inspector -> Table View Cell -> identifierntg属性上设置:cell;

<img src="/images/a6.png">

###(5) Add TableViewCell.swift

为界面添加程序类TableViewCell.swift;

<img src="/images/b1.png">

<img src="/images/b2.png">

<img src="/images/b3.png">

将设计界面与程序类关联: 选取左侧面板View Controller Scene -> View Controller -> View -> Table View -> cell, 再选取右侧面板Identifier Inspector -> Custom Class -> Class, 设置为: TableViewCell

<img src="/images/b4.png">

###(6) Add Label and Button to ViewController -> ... -> cell

从右下角的object library中选取Label对象并拖进cell界面上,居左放置;

从右下角的object library中选取Button对象并拖进cell界面上,居右放置,改名为Log;

在左侧面板选择cell,在右侧面板上选Attributes -> Table View Cell -> Accessory,设置为Disclosure Indicator;

在下方靠右工具栏中选择Resolve Auto Layout Issue -> Add Missing Contraints;

<img src="/images/c1.png">

<img src="/images/c2.png">

###(7) 打开Associate Editor,给TableViewCell.swift添加插座,并将Label:titleLabel,Log:shareButton插入;

<img src="/images/c6.png">

###(8) 给Table View 添加 dataSource , delegate

在左侧面板选择Table View,在右侧选择Connections Inspector,将dataSource拉进界面上进行连接,再从界面上点击Table View区域拉进到View Controller上,选择delegate;

<img src="/images/c3.png">

<img src="/images/c4.png">

###(9) 给ViewController.swift添加插座,将Table View界面插入;

<img src="/images/c5.png">

###(10) 创建NewViewController.swift类,并将第二个设计界面(New View Controller)与其关联

<img src="/images/d1.png">

<img src="/images/d2.png">

选择第二个设计界面(New View Controller Scene),添加Label控件,Add Missing Constraints;

<img src="/images/d3.png">

打开Associate Editor,为NewViewController.swift添加插座,并插入titleLabel;

<img src="/images/d4.png">

##3 处理程序

###(1) NewViewController.swift

添加titleString:

    import UIKit
    
    class NewViewController: UIViewController {
    
        @IBOutlet weak var titleLabel: UILabel!
        
        var titleString: String!
        
        override func viewDidLoad() {
            super.viewDidLoad()
    
            self.titleLabel.text = self.titleString
            
        }
    
        override func didReceiveMemoryWarning() {
            super.didReceiveMemoryWarning()
            // Dispose of any resources that can be recreated.
        }
   
    }

###(2) ViewController.swift 事件处理程序

    import UIKit
    
    class ViewController: UIViewController,UITableViewDataSource,UITableViewDelegate {
        
        @IBOutlet weak var tableView: UITableView!
        
        var objects: NSMutableArray! = NSMutableArray()
        
        override func viewDidLoad() {
            super.viewDidLoad()
            
            self.objects.addObject("iPhone")
            self.objects.addObject("Apple Watch")
            self.objects.addObject("Mac")
            
            self.tableView.reloadData()
        }
        
        override func didReceiveMemoryWarning() {
            super.didReceiveMemoryWarning()
            // Dispose of any resources that can be recreated.
        }
        
        //MARK: Table View
        
        func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
            return self.objects.count
        }
        
        func tableView(tableView: UITableView, cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {
            let cell = self.tableView.dequeueReusableCellWithIdentifier("cell", forIndexPath: indexPath) as! TableViewCell
            cell.titleLabel.text = self.objects.objectAtIndex(indexPath.row) as? String
            cell.shareButton.tag = indexPath.row
            cell.shareButton.addTarget(self, action: "logAction:", forControlEvents: .TouchUpInside)
            
            return cell
        }
        
        func tableView(tableView: UITableView, didSelectRowAtIndexPath indexPath: NSIndexPath) {
            self.performSegueWithIdentifier("showView", sender: self)
        }
        
        @IBAction func logAction(sender:UIButton){
            let titleString = self.objects.objectAtIndex(sender.tag) as? String
            
            let firstActivityItem = "\(titleString)"
            
            let activityViewController: UIActivityViewController = UIActivityViewController(activityItems: [firstActivityItem], applicationActivities: nil)
            
            self.presentViewController(activityViewController, animated: true, completion: nil)
        }
        
        override func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject?) {
            if(segue.identifier == "showView"){
                var upcoming: NewViewController = segue.destinationViewController as! NewViewController
                
                let indexPath = self.tableView.indexPathForSelectedRow()!
                
                let titleString = self.objects.objectAtIndex(indexPath.row) as? String
                
                upcoming.titleString = titleString
                
                self.tableView.deselectRowAtIndexPath(indexPath, animated: true)
            }
        }
        
    }

##4 编译运行

<img src="/images/e1.png">

点击Log:

<img src="/images/e2.png">

<img src="/images/e3.png">

点击 >:

<img src="/images/e4.png">


