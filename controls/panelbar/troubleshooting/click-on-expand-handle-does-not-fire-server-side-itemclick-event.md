---
title: Click on Expand Handle Does Not Fire Server-Side ItemClick Event
page_title: Click on Expand Handle Does Not Fire Server-Side ItemClick Event | UI for ASP.NET AJAX Documentation
description: Click on Expand Handle Does Not Fire Server-Side ItemClick Event
slug: panelbar/troubleshooting/click-on-expand-handle-does-not-fire-server-side-itemclick-event
tags: click,on,expand,handle,does,not,fire,server-side,itemclick,event
published: True
position: 1
---

# Click on Expand Handle Does Not Fire Server-Side ItemClick Event



## Click on Expand/Collapse Handle Does Not Fire Server-Side ItemClick Event

__PROBLEM__

If I click on the Expand/Collapse button of the RadPanelItem the ItemClick never fires.

__EXPLANATION__

In general expanding and collapsing RadPanelItems is entirely a client-side functinality. It is implemented for scenarios when __NavigateUrl__ property of the item is set. The expand/collapse handle enables a user to expand and collapse the item whithout navigating to the assigned page. It is intended by design that clicking the handle neither performs a postback of the page not triggers any of the RadPanelBar events.

__WORKAROUND__

Below you can find several workarounds to enable the server side ItemClick event when expanding/collapsing a RadPanelItem.

1. Hide the expand/collapse handle using css:

````XML
	        .rpExpandHandle
	        {
	            display: none !important;
	        }
````



1. Force a PostBack of the page when a RadPanelItem is clicked:

````ASPNET
	        function onClientCollapseExpand(sender, args) {
	            var handler = $telerik.$('span.rpExpandHandle');
	            //get the clicked handler element
	            if (handler) {
	                //perform postback
	                __doPostBack();
	            }
	            else {
	                //do something else
	            }
	        }
````



````ASPNET
	    <telerik:radpanelbar runat="server" id="RadPanelBar1" onclientitemcollapse="onClientCollapseExpand"
	        onclientitemexpand="onClientCollapseExpand">
	                <Items>
	                    <telerik:RadPanelItem Text="Item1">
	                        <Items>
	                            <telerik:RadPanelItem Text="Item1">
	                            </telerik:RadPanelItem>
	                            <telerik:RadPanelItem Text="Item2">
	                            </telerik:RadPanelItem>
	                        </Items>
	                    </telerik:RadPanelItem>
	                    <telerik:RadPanelItem Text="Item2">
	                    </telerik:RadPanelItem>
	                    <telerik:RadPanelItem Text="Item3">
	                    </telerik:RadPanelItem>
	                </Items>
	            </telerik:radpanelbar>
````

