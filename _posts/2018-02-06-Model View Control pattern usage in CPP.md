---
layout: post
excerpt_separator: <!--more-->
title: "Model View Control (MVC) pattern usage in C++"
date: 2018-02-06
tags: design-pattern MVC C++
---

MVC (Model-View-Controller) pattern is often used in Web based applications, where "View" is your actual HTML content displayed on browser, where as "Controller" is the code that gather dynamic data and generates content within the HTML. Finally, "Model" talks about actual content, probably stored in DataBase or XML, and your business rules transform these contents based on user actions. <!--more-->
As I mentioned, MVC is most widely used in web based applications, but some how I liked this pattern and tried using it in my C++ application.
Scenario is, I have a module in C++ which generates set of System Information, and displays them to user. Since, they are system information, they keep change, and I have to update at view the same. Hope you understood.

Since I cannot get you what I wrote in my module, but I can surely show you a sample code, (the code is simple and self explanatory) 

``` C++

/* * * * * * * * * * * * * * *
* File       : mvc-class.cpp
* Author     : Kiran Puranik
* Copyrights : no copy rights :)
* 
* * * * * * * * * * * * * * */
#include <iostream>

using namespace std;

/* Model class */
class SystemInfoModel {
    
private:
    string m_InfoName;
    string m_InfoValue;
    
public:
    string Get_InfoName (void) {
        return m_InfoName;
    }
    
    string Get_InfoValue (void) {
        return m_InfoValue;
    }
    
    void Set_InfoName (string info_name) {
        if (!info_name.empty()) {
            m_InfoName = info_name;
        }
    }
    
    void Set_InfoValue (string info_val) {
        if (!info_val.empty()) {
            m_InfoValue = info_val;
        }
    }
};

/* View class */
class SystemInfoView {

public:
    void Print_SystemInfo (string name, string val) {
        cout << "|---------------------------------|" << endl;
        cout << "|    System Info    |    Value    |" << endl;
        cout << "|---------------------------------|" << endl;
        cout << "|   " << name << "    |   " << val << "   |" << endl;
    }
};

/* Controller class*/
class SystemInfoController {

private:
    SystemInfoModel m_SysModel; //\ reference for Model and View
    SystemInfoView  m_SysView;  ///
    
public:
    /* CTR */
    SystemInfoController (SystemInfoModel si_model, SystemInfoView si_view) {
        m_SysModel = si_model;
        m_SysView  = si_view;
    }
    
    /* User control APIs */
    void Set_SystemInfo_Name (string si_name) {
        if (!si_name.empty()) {
            m_SysModel.Set_InfoName (si_name);
        }
    }
    
    void Set_SystemInfo_Value (string si_val) {
        if (!si_val.empty()) {
            m_SysModel.Set_InfoValue (si_val);
        }
    }
    
    string Get_SystemInfo_Name (void) {
        return m_SysModel.Get_InfoName();
    }
    
    string Get_SystemInfo_Value (void) {
        return m_SysModel.Get_InfoValue();
    }
    
    /* Now, bind the Model with View */
    void Update_System_Info (void) {
        m_SysView.Print_SystemInfo (m_SysModel.Get_InfoName(), m_SysModel.Get_InfoValue());
    }
};

/* Now, usage part of it ----------- */
int main ()
{
    // system info model instatiation
    SystemInfoModel siModel;
    siModel.Set_InfoName ("Memory Usage"); // looks dirty isn't it. But usually they are
    siModel.Set_InfoValue ("1024 KB");   // fetched from system units/or other utilities
    
    // system info view instatiation
    SystemInfoView  siView;
    
    // now, the controller
    SystemInfoController siControl (siModel, siView);
    
    // let's display the content now
    siControl.Update_System_Info ();
    
    // now, the system info has changed, value is different
    siControl.Set_SystemInfo_Value ("2048 KB");
    
    // and display updated content
    siControl.Update_System_Info ();
    
    // isn't it a great pattern !!!!
    
    return 0;
}

```