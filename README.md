# Comparative Study of Countries' Insurance (Tableau Dashboard)

## Overview

This repository contains the steps and potentially the final Tableau Public workbook for a comparative study of countries' insurance markets. The analysis utilizes two datasets: an "Insurance Sample Dataset" and the "Global Financial Development Database (July 2018)". The resulting Tableau dashboard allows for interactive exploration and comparison of various insurance-related metrics across different countries and income levels.

## Steps to Recreate the Tableau Dashboard

This section outlines the step-by-step process to build the Tableau dashboard.

**1. Connect to Data Sources:**

1.  **Open Tableau Public.**
2.  On the home page, under **Connect**, in the **To a File** section, click **Excel**.
3.  Browse to and select the **Insurance Sample Dataset Excel file** as the primary data source.
4.  Click the **Add** button to connect to a secondary data source.
5.  Browse to and select the **Global Financial Development Database - Jul2018 Excel file**.
6.  In the canvas area, drag and drop the relevant tables (likely named "Data July 2018" or similar) from the Global Financial Development Database. Tableau will attempt to establish relationships between the datasets.

**2. Create the Map Visualization (Sheet: MAP):**

1.  Go to **Sheet 1** and rename it to **MAP**.
2.  From the **Insurance Sample Dataset**, drag the **Country** field to the **Detail** mark card.
3.  On the **Marks** card, change the **Automatic** mark type to **Map**.
4.  From the **Global Financial Development Database**, drag the **Income** dimension to the **Filters** shelf. Select **All** in the filter dialog and click **Show Filter**.
5.  Drag the **Income** dimension to the **Color** mark card.
6.  Drag the **Iso3** field (likely representing country codes) to the **Label** mark card.

**3. Create the Key Performance Indicator (KPI) Table (Sheet: KPI):**

1.  Rename **Sheet 2** to **KPI**.
2.  **Create Calculated Fields for Comparison:**
    * Define two calculated fields to determine the values for the selected period and the period prior. These calculations will likely involve using parameters for year selection.
3.  **Create Parameters:**
    * Create a parameter named **Year Selection** (likely an integer or date type).
    * Create a parameter named **Category Selection** (likely a string type with a list of values).
    * The **Category Selection** parameter should include the following options:
        * life insurance share
        * market share
        * penetration
        * ratio of reinsurance accepted
        * retention ratio
4.  **Build the KPI Table:**
    * Drag **Measure Names** to the **Rows** shelf. Filter **Measure Names** to include the calculated fields representing the "Selected Period" value and the "Category value" (driven by the Category Selection parameter) for comparison. Also include a calculated field for "Growth %".
    * Convert the aggregation of the "Selected Period" and "Category value" measures from **Sum** to **Average**.
    * Drag **Measure Values** to the **Text** mark card.

**4. Create Growth Indicators:**

1.  Create two calculated fields:
    * **Growth Color:** This field will determine the color of the growth indicator (e.g., green for positive growth, red for negative). It will likely use a conditional statement comparing the selected period's value with the prior period's value.
    * **Growth Indicator:** This field will display a visual indicator of growth (e.g., an up or down arrow) based on the comparison between the selected and prior periods. It will also likely use a conditional statement.
2.  Drag the **Growth Color** calculated field to the **Color** mark card.
3.  Drag the **Growth Indicator** calculated field to the **Text** mark card.

**5. Create the Trend Chart (Sheet: Trend Chart):**

1.  Rename the next sheet to **Trend Chart**.
2.  Show both the **Year Selection** and **Category Selection** parameters by right-clicking on them in the **Data** pane and selecting **Show Parameter Control**.
3.  Drag the **Year** dimension to the **Columns** shelf.
4.  Drag the measure corresponding to the **Category Selection** parameter to the **Rows** shelf. Change its aggregation from **Sum** to **Average**.
5.  Drag the **Year** dimension to the **Pages** shelf to create a motion chart.
6.  On the **Pages** shelf, click on **Show History** and enable **Trails** to visualize the trend over time.

**6. Create the Dashboard:**

1.  Click on the **Dashboard** button at the bottom of the Tableau window.
2.  In the **Size** pane (on the left), click **Automatic** to make the dashboard responsive.
3.  Add **Horizontal** and **Vertical** layout containers to organize the dashboard elements.
4.  Drag the **MAP** sheet onto the dashboard.
5.  From the **Objects** pane (on the left), drag a **Web Page** object onto the dashboard.
6.  **Set up URL Action for Map Interaction:**
    * Go to **Dashboard** in the top menu, then select **Actions...**.
    * Click **Add Action** and choose **Go to URL...**.
    * **Edit Action:**
        * **Source Sheets:** Select the **MAP** sheet.
        * **Run action on:** Choose **Select**.
        * In the **URL** bar, enter the desired web page URL (e.g., a country profile on Wikipedia) and ensure you append relevant parameters to make it dynamic based on the selected country. For example, if your URL is `https://en.wikipedia.org/wiki/`, you might append `<Country>`. **Note:** The exact syntax for passing parameters depends on the target website.
        * Click **OK**.
7.  Drag the **KPI** sheet, the sheet containing the **Growth Indicator**, and the **Trend Chart** sheet onto the dashboard and arrange them as desired.

**7. Add Dashboard Filters:**

1.  On the dashboard, right-click on the **Income Filter** (the filter you showed on the **MAP** sheet).
2.  Select **More options** and then **Apply to Worksheets**.
3.  Choose **Selected Worksheets...** and then select **All on Dashboard** to make the income filter control the data across all sheets in the dashboard.

**8. Create Dashboard Filter Actions (Optional but Recommended for Interactivity):**

1.  Go to **Dashboard** in the top menu, then click **Actions...**.
2.  Click **Add Action** and choose **Filter...**.
3.  **Edit Filter Action:**
    * **Source Sheets:** Select the sheet that should initiate the filtering (e.g., the **MAP** sheet).
    * **Run action on:** Choose **Select**.
    * **Target Sheets:** Select the other sheets on the dashboard that should be filtered.
    * Define how the filter should work (e.g., based on the selected **Country**).
    * Click **OK**.
