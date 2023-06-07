# Revenue_Insights_OYO_hotels
This project starts with the downloading of the dataset from kaggle. Tis was an excel data that is constitute of five sheets:
* dim_date: date, date type, week number
* dim_hotel: category, city, property id, property name
* dim_rooms: room class, room id
* fact_aggerated_booking:check in date, property id, room category, successful booking, capacity
* fact_booking: no guest, ratings given, property id, booking date, booking id, booking platform, booking status, check in date, room category, revenue generated, revenue relized
# key Matrix using DAX
* ADR = DIVIDE( [Revenue], [Total Bookings],0)

* ADR WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([ADR],dim_date[wn]= selv)
var revpw =  CALCULATE([ADR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))
return
DIVIDE(revcw,revpw,0)-1

* Average Rating = AVERAGE(fact_bookings[ratings_given])

* Booking % by Platform = DIVIDE([Total Bookings],
 CALCULATE([Total Bookings], 
 ALL(fact_bookings[booking_platform])
  ))*100
  
  * Booking % by Room class = DIVIDE([Total Bookings],
 CALCULATE([Total Bookings], 
 ALL(dim_rooms[room_class])
  ))*100
  
  * DURN = DIVIDE([Total Checked Out],[No of days])
  * No of days = DATEDIFF(MIN(dim_date[date]),MAX(dim_date[date]),DAY) +1
  * No Show rate % = DIVIDE([Total no show bookings],[Total Bookings])
  * Occupancy % = DIVIDE([Total Succesful Bookings],[Total Capacity],0)
  
  
