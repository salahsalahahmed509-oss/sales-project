import pandas as pd
import matplotlib.pyplot as plt
import seaborn as ans 
plt.style.use("ggplot")

df = pd.read_csv(r"C:\Users\20100\Downloads\sales_data.csv")
df.dropna(inplace=True)

Top_SalesPerson = df.groupby("Sales_Rep")["Sales_Amount"].sum().sort_values(ascending=False)
Top_region = df.groupby("Region")["Sales_Amount"].sum().sort_values(ascending=False)
Top_product = df.groupby("Product_ID")["Sales_Amount"].sum().sort_values(ascending=False)
Top_customer = df.groupby("Customer_Type")["Sales_Amount"].sum().sort_values(ascending=False)

fig, axes = plt.subplots(2, 2, figsize=(15, 10))

fig.suptitle("Sales Data Analysis Dashboard", fontsize=18)

Top_SalesPerson.head(5).plot(kind="bar", ax=axes[0, 0], color="steelblue", title="Top Sales Persons")
axes[0, 0].set_xlabel("Sales Rep")
axes[0, 0].set_ylabel("Sales Amount")

Top_region.head(5).plot(kind="bar", ax=axes[0, 1], color="green", title="Top Regions")

Top_product.head(5).plot(kind="bar", ax=axes[1, 0], color="orange", title="Top Products")

Top_customer.head(5).plot(kind="bar", ax=axes[1, 1], color="purple", title="Top Customers")

plt.tight_layout()
plt.show()