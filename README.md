# Repo-create
Q.1
function getPincodeDetails(pincode) {
  var url = "https://api.postalpincode.in/pincode/" + pincode;
  var response = UrlFetchApp.fetch(url);
  var data = JSON.parse(response.getContentText());

  if (data[0].Status == "Success") {
    var post = data[0].PostOffice[0];

    return {
      Pincode: pincode,
      District: post.District,
      State: post.State,
      Region: post.Region
    };
  } else {
    return {
      Error: "Invalid Pincode"
    };
  }
}


Q.2
import pandas as pd

shipment = pd.read_csv("Shipment_Data.csv")
rate = pd.read_csv("Rate_Card.csv")

data = pd.merge(shipment, rate, on="Pincode")

data["Cost"] = (
    data["Shipment Weight"] *
    data["Rates at Per Kg Level"] +
    data["LR Charges"]
)

print(data[["Pincode", "Cost"]])

data.to_csv("Updated_Shipment.csv", index=False)

Pip instalation
pip install gspread pandas oauth2client

import gspread
from oauth2client.service_account import ServiceAccountCredentials
