# ag-framework for mobile automation testing

An automation mobile testing framework based on python(3.8) and Appium (latest). This development based on interview with QA, that want to easily create mobile testing automation. 
Then I try to make it easier for each line and step inspired by robotframework that used for web. AG stand for automation great, or automation gartanto or ashary gartanto haha :D Step :

1. install python 3.8
2. install Appium client (pip install Appium-Python-Client)
3. install ag-framework --> https://test.pypi.org/project/ag-framework/0.1.2/
   
   'pip install -i https://test.pypi.org/simple/ ag-framework==0.1.2' --> for this release will be updated later
4. Add in main.py :
   
    import library :
   
      from modules.ag_interpreter import AgInterpreter
   
      from modules.actions import execute_actions
   
    change main to :
   
       if __name__ == "__main__":
   
          interpreter = AgInterpreter('main.ag')
   
          execute_actions(interpreter)

6. if you will record testing in video. Please create 'screenshot' folder in same layer with main.py

The template can be generated by using command : 

'ag generate -f <filename.ag>' 

this sample will generate sample application to open calculator and run 1 + 1 = 2 

To see the command use command : 
'ag help'

The sample ag-framework : first segment is Capabilities to connect to appium. 

Please refer to this : https://appium.io/docs/en/2.1/quickstart/install/ and run appium server in command

# first segment is setting capabilities
for capabilities can have look to this : https://appium.io/docs/en/2.1/guides/caps/


#main.ag

*** Desired Capabilities *** 

platformName = Android 

deviceName = emulator-5554

#gmail

appPackage = com.google.android.gm 

appActivity = com.google.android.gm.ConversationListActivityGmail

automationName = UiAutomator2 

autoGrantPermissions = true 

noReset = true 

desired_cap:

    platformName
    
    deviceName
    
    appPackage
    
    appActivity
    
    automationName
    
    autoGrantPermissions
    
    noReset
    
*** End Desired Capabilities ***

# second segment is setting variable

#Settings section with additional settings (in this case, the URL).

*** Settings *** url = 'http://localhost:4723' *** End Settings ***

# third segment is connect to appium

#Connect Capabilities Block contains the code to connect to the Appium server with the specified capabilities.

*** Connect Capabilities *** 

driver = webdriver.Remote(url, options=AppiumOptions().load_capabilities(desired_cap)) 

*** End Connect Capabilities ***

# fourth segment is execution step this sample is sending mail by gmail

#Execution Block contains the steps for the automation, such as interacting with the app.

*** Execution ***

Record_Start Sleep 3 

Scroll_To_Bottom 1 

Click_Button Compose 

Set_Implicit_Wait 3 

Sleep 3 

Send_Text_Focus ashary_g@yahoo.co.id 

Sleep 1 

Press_Enter_Key 

Sleep 1 

Press_Enter_Key 

Input_Edit_Text Subject subject test2 

Sleep 1 

Press_Enter_Key 

Sleep 2 

Click_Edit_Text Compose email 

Sleep 2 

Send_Text_Focus 

ini email testing 

Sleep 1 

Send_Enter_Text_Focus 

Sleep 1 

Send_Text_Focus garis baru 

Sleep 2 

Click_Button Send 

Sleep 3 

Record_Stop test_gmail_send

*** End Execution ***

# note : 
*** --> for begin and end each segment

\#1 line comment

/* start comment 
multi comment 
*/ end comment

# Execution function and parameters for now there are 16 actions, will continue updating :
  Set_Implicit_Wait: Set the implicit wait time for finding elements. Parameter (second)
  
  Click_Button: Click a button with the specified label. Parameter (label button name)
  
  Click_Text_View: Click a text view (non editable text) with the specified text. Parameter (label name)
  
  Click_Edit_Text: Click an edit text field with the specified label. Parameter (label name)
  
  Input_Edit_Text: Enter text into an edit text field. Parameter (label name,  value)
  
  Clear_Text: Clear the text from the currently focused element.
  
  Send_Text_Focus: Send text to the currently focused element. Parameter (value)
  
  Press_Enter_Key: Simulate pressing the Enter key.
  
  Press_Tab_Key: Simulate pressing the Tab key.
  
  Sleep: Pause execution for a specified duration. Parameter (second)
  
  Scroll_To_Bottom: Scroll to the bottom of the screen. Parameter (number how many times scroll to bottom)
  
  Scroll_To_Top: Scroll to the top of the screen. Parameter (number how many times scroll to top)
  
  Swipe_Up: Swipe up on the screen. Used for example in android to open menu
  
  Record_Start: Start recording actions for automation. Pair with Record_Stop in the last step that want to be recorded. To use this create folder screenshot in same path with main
  
  Record_Stop: Stop recording actions and save the recorded script. Parameter (filename without extension) To use this create folder screenshot in same path with main
  
  Send_Enter_Text_Focus: Send the Enter key to the currently focused element.
  
Authors
@asharygartanto
