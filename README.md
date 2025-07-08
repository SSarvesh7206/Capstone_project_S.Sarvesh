# Capstone_project_S.Sarvesh

Model_1:



Basic Linear Model



Logic-

Occupancy rate=Occupancy/Capacity in the given window(I have taken it to be 30 minutes)

price=
	
      10*(1+Occupancy rate)  if Avg. value of Occupancy rate in that window is greater than 0.7

      10*(1+0.7*Occupancy rate)   if Avg. value of Occupancy rate in that window is greater than 0.5, less than 0.7
	
      10*(1+0.5*Occupancy rate)   if Avg. value of Occupancy rate in that window is greater than 0.3, less than 0.5
	
      else: 10 (i.e) base price
	
      [LOGIC APPLIED USING THE pw.if_else(else_clause,then_clause,else_clause) FUCNTION OF PATHWAY API]
	
Output Bokeh Plot-
![Model_1_plot](https://github.com/user-attachments/assets/66d9312a-f7d4-401d-9c1c-907fd2be3b9e)


Model_2:

Demand based model

Logic-

Encoding done:

For vehicle type-

cycle=1,bike=2,car=3,truck=4

For Traffic-

low=1,average=2.high=3

Special day-

Yes=1,No=2

Occupancy rate=Occupancy/Capacity in the given window(I have taken it to be 30 minutes)

vehType=Avg. value of vehicle type in that window(30 minutes)

traffic=Maximum value of traffic in the window

special=Value of IsSpecialDay

queue=Max queue length observed in the window

To normalize, dividing each feature's value in the window by its maximum value possible(4-For vehicle type,3-Traffic,15-queue) and dividing the final demand expression by the number of features used in it is done to ensure that finally the value of the demand is in the range of 0 to 1.


     When queue>13-demand=((vehtype/4)-(traffic/3)^2+(2*special)+(occupancy rate)+(queue/15)^0.5)/5

                   price=10*(1+0.8*demand)
		  
     queue<=13 and queue>10-demand=((vehtype/4)-(traffic/3)^2+(2*special)+(occupancy rate)+(queue/15)^0.75)/5
     
                            price=10*(1+0.8*demand)
				    
     queue<=10 and queue>5-demand=((vehtype/4)-(traffic/3)^2+(2*special)+(occupancy rate)+(queue/15))/5
     
                           price=10*(1+0.6*demand)
				   
     queue<=5 and queue>3-demand=((vehtype/4)+(occupaancy rate)+special)/3
     
                          price=10*(1+0.5*demand)
				  
     queue<3-price=10(Base price)
     
     [LOGIC APPLIED USING THE pw.if_else(else_clause,then_clause,else_clause) FUCNTION OF PATHWAY API]
     
Output Bokeh plot-
![Model_2_plot](https://github.com/user-attachments/assets/24c7f484-f6f1-4880-b32f-b151efdc5abe)
