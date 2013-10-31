
Dashboard
=========

The RockStor dashboard is a view for an admin to rapidly monitor the storage, compute and network resources of the appliance. 

The dashboard is designed as a configurable set of widgets, each displaying some information about the resources mentioned above. The admin can select which widgets to display from the left sidebar that displays the list of available widgets, and can arrange the widgets by dragging them to required positions. A widget can be removed from the dashboard by clicking the X icon on the top right of the widget.

   .. image:: dashboard-conf.gif
      :scale: 60 % 
      :align: center

Dashboard Widgets
-----------------
Widgets have two states, compact and expanded. They can be toggled between the two states by clicking the resize icon located at the top right of each widget.
The compact state displays minimal information required for monitoring a particular resource, and the expanded state displays more detail, and may have more functionality like viewing history of the resource etc.

The individual widgets are described below.

CPU
___

  The CPU widget displays the cpu usage of the appliance and is updated every second. The widget display is divided into two parts. 
  The top graph displays the percent of time spent in system mode, user mode, and user mode nice, for each cpu, for the current time interval. 
  The bottom graph displays the percentage of average time spent in each mode over all cpus, over the last 5 minutes.

   .. image:: cpu-widget.png
      :align: center

Memory
______

The memory widget displays a graph of memory usage over the last 5 minutes.

   .. image:: memory-widget.png
      :align: center

Disk activity
_____________

The disk activity widget displays the top 5 disks sorted by read/write activity. Activity can be sorted by reads, writes or both. 

Network activity
________________

The network activity widget displays data sent/received, and packets sent/received over the selected network interface, over the last 5 minutes.

   .. image:: network-widget.png
      :align: center


