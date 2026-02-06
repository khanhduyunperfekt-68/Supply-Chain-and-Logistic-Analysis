**Total Sales** = SUM(SalesFINAL12312016\[SalesAmount])



**Total Sales Quantity** = SUM(SalesFINAL12312016\[SalesQuantity])



**SalesAmount** = SalesFINAL12312016\[SalesQuantity] \* SalesFINAL12312016\[SalesDollars]



**Reorder Point** = 

VAR DailyDemand = \[Total Sales] / 60 

VAR LeadTime = 7 

VAR SafetyStock = DailyDemand \* 3 

RETURN

(DailyDemand \* LeadTime) + SafetyStock



**Purchase to Sales Ratio =** 

DIVIDE(\[Total Purchases], \[Total Sales], 0)



**Gross Profit** = \[Total Sales] - \[Total Purchases]



**Sale fore cast** = GENERATESERIES(-0.5, 0.5, 0.05)



**Forecast Sales March** = 

VAR AvgSalesFeb = 

&nbsp;   CALCULATE(

&nbsp;       AVERAGEX(VALUES('DateTable'\[Date]), \[Total Sales]),

&nbsp;       DATESBETWEEN('DateTable'\[Date], DT"2016-02-01", DT"2016-02-29")

&nbsp;   )

RETURN

AvgSalesFeb \* 31



**Forecast Sale Adjusted** = \[Forecast Sales March] \* (1 + \[Growth Percentage Value])



**Total Purchases** = SUM(PurchasesFINAL12312016\[Dollars])



**LowInventory** =

    CALCULATE(

        COUNTROWS(EndInvFINAL12312016),

        EndInvFINAL12312016\[onHand] <= 5

    )



**LowInventoryRate** = 

&nbsp;   DIVIDE(

&nbsp;       \[LowInventory], 

&nbsp;       COUNTROWS(EndInvFINAL12312016)

&nbsp;   )



**Inventory Variance** = \[Ending Inventory] - \[Beginning Inverntory]



**Growth Percentage** = GENERATESERIES(-0.5, 0.5, 0.05)



**DateTable** = CALENDAR(MIN(SalesFINAL12312016\[SalesDate]), MAX(SalesFINAL12312016\[SalesDate]))



**Ending Inventory** = SUM(EndInvFINAL12312016\[onHand])



**Beginning Inverntory** = Sum(BegInvFINAL12312016\[onHand])







