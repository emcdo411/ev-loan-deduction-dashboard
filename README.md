# 🚘 ev-loan-deduction-dashboard

> *PowerBI-style RShiny app for EV loan deduction tracking, built to support CRM logic and real-time dealership marketing.*

---

## 📌 [Summary](#summary)

This dashboard showcases how car dealerships — like Cox Automotive, Carvana, and Autonation — can target and communicate with car buyers who qualify for the **new EV loan interest deduction**, a major part of the 2025 green energy bill.

Designed with Microsoft Fabric-inspired UI, the app offers:

* 🔐 CRM-style login simulation
* 🌗 Dark/light mode toggle
* 📈 Interactive dashboard visualizations
* 📤 Exportable filtered data
* 🔧 API-ready logic for CRM or DMS integration

---

## 🧰 [Tech Stack](#tech-stack)

![R Shiny](https://img.shields.io/badge/Frontend-R_Shiny-00BFC4?style=for-the-badge)
![ShinydashboardPlus](https://img.shields.io/badge/UI-shinydashboardPlus-4682B4?style=for-the-badge)
![Plotly](https://img.shields.io/badge/Charts-Plotly-F7931E?style=for-the-badge)
![DT](https://img.shields.io/badge/Tables-DT-2496ED?style=for-the-badge)
![ShinyJS](https://img.shields.io/badge/JS%20Logic-shinyjs-FF4500?style=for-the-badge)
![ShinyWidgets](https://img.shields.io/badge/UX-shinyWidgets-DA70D6?style=for-the-badge)
![ShinyFeedback](https://img.shields.io/badge/Validation-shinyFeedback-F4C542?style=for-the-badge)

---

## 📊 [What the App Does](#what-the-app-does)

| Feature                  | Functionality                                           |
| ------------------------ | ------------------------------------------------------- |
| 🔐 Dealer Login          | Username/password for simulated CRM entry               |
| 💡 Price Filters         | Live filtering under \$55K with sliders and checkboxes  |
| 📊 PowerBI-Styled Graphs | Interactive bar + pie charts (built with Plotly)        |
| 📤 Export to CSV         | Download filtered datasets instantly                    |
| 🌗 Theme Toggle          | Switch between light and dark Microsoft Fabric themes   |
| ✅ No CSVs Needed         | Uses hardcoded data for standalone demo                 |
| 🛠️ API-Ready            | Framework includes logic for future CRM/API integration |

---

## 🔄 [What’s Coming with API Integration](#what’s-coming-with-api-integration)

When CRM or dealership APIs are connected, this dashboard will also:

* 💬 Show real-time buyer leads by zip code
* 📡 Trigger auto emails/SMS based on customer profile
* 🧠 Suggest qualifying cars based on credit/income
* 📈 Track marketing campaign results in real-time
* 🔌 Sync with dealership inventory via DMS or FastAPI

---

## 💡 [Why This Matters](#why-this-matters)

Car buyers can now deduct interest from EV loans on cars under \$55K — **but few know about it.**

Car dealers don’t need \$100K marketing budgets to reach those customers. This app proves that **smart data logic, a clean UI, and API-aware thinking** can get you most of the way there — using **free tools like RShiny.**

In short: **It’s PowerBI for car loan marketing — with AI-ready infrastructure.**

---

## 🔐 [Login Demo](#login-demo)

* **Username:** `dealer`
* **Password:** `ev123`

---

## 🧪 [How to Run This Project](#how-to-run-this-project)

1. 📦 Install required R packages:

```r
install.packages(c("shiny", "shinydashboard", "shinydashboardPlus", "shinyjs", "plotly", "DT", "shinyWidgets", "shinyFeedback"))
```

2. 🛠️ Open RStudio and paste the **full code below** into a file called `app.R`.

3. ▶️ Run the app:

```r
shiny::runApp()
```

---

## 📁 [Optional: Folder Structure](#optional-folder-structure)

```
ev-loan-deduction-dashboard/
├── app.R                  # (full code below)
├── README.md
└── assets/                # (optional for logos or themes)
```

---

## 🧠 [Author](#author)

**Maurice McDonald**
Microsoft Software & Systems Academy – Cloud Application Development Cohort
📧 [erwin.mcdonald@outlook.com](mailto:erwin.mcdonald@outlook.com)
💼 [linkedin.com/in/mauricemcdonald](https://linkedin.com/in/mauricemcdonald)
💻 [github.com/emcdo411](https://github.com/emcdo411)

---

## 📦 [# Load libraries
required_packages <- c("shiny", "shinydashboard", "shinydashboardPlus", "shinyjs", "plotly", "DT", "shinyWidgets", "shinyFeedback")
for (pkg in required_packages) {
  if (!requireNamespace(pkg, quietly = TRUE)) {
    tryCatch({
      install.packages(pkg, dependencies = TRUE, repos = "https://cran.rstudio.com/", quiet = TRUE)
      cat("Installed package:", pkg, "\n")
    }, error = function(e) {
      cat(sprintf("Failed to install %s: %s\n", pkg, conditionMessage(e)))
    })
  }
  tryCatch({
    suppressPackageStartupMessages(library(pkg, character.only = TRUE))
    cat("Loaded package:", pkg, "version:", packageVersion(pkg), "\n")
  }, error = function(e) {
    cat(sprintf("Failed to load %s: %s; using fallback if applicable\n", pkg, conditionMessage(e)))
  })
}

# Check shinydashboardPlus availability and version
use_shinydashboardPlus <- requireNamespace("shinydashboardPlus", quietly = TRUE)
if (use_shinydashboardPlus) {
  shinydashboardPlus_version <- packageVersion("shinydashboardPlus")
  cat("shinydashboardPlus version:", as.character(shinydashboardPlus_version), "\n")
} else {
  cat("shinydashboardPlus not available; using shinydashboard::box\n")
}

# Hardcoded car data under $55,000 (expanded for demo)
car_data <- data.frame(
  Dealer = c("Autonation", "Carvana", "Cox Automotive", "Autonation", "CarMax", "Lithia Motors", "Carvana", "Cox Automotive", "Autonation", "CarMax"),
  Make = c("Toyota", "Hyundai", "Ford", "Chevrolet", "Tesla", "Honda", "Nissan", "Kia", "Volkswagen", "Rivian"),
  Model = c("Camry Hybrid", "Ioniq 6", "Escape Hybrid", "Bolt EUV", "Model 3", "Accord Hybrid", "Leaf", "Niro EV", "ID.4", "R1S"),
  Price = c(33000, 45000, 39500, 27500, 42000, 34000, 28000, 39000, 41000, 52000),
  Year = c(2024, 2024, 2023, 2023, 2024, 2024, 2023, 2024, 2024, 2025),
  FuelType = c("Hybrid", "EV", "Hybrid", "EV", "EV", "Hybrid", "EV", "EV", "EV", "EV"),
  Range = c(600, 340, 550, 247, 272, 580, 212, 253, 260, 300),
  stringsAsFactors = FALSE
)

# UI
ui <- dashboardPage(
  skin = "black",
  dashboardHeader(title = span("EV Loan Deduction Tracker", style = "font-weight: bold; font-family: Roboto;")),
  dashboardSidebar(
    useShinyjs(),
    sidebarMenu(
      id = "tabs",
      menuItem("Login", tabName = "login", icon = icon("user-lock")),
      menuItem("Dashboard", tabName = "dashboard", icon = icon("chart-line")),
      menuItem("Eligible Cars", tabName = "cars", icon = icon("car")),
      menuItem("About", tabName = "about", icon = icon("info-circle"))
    ),
    hr(),
    div(
      style = "padding: 10px;",
      prettyCheckboxGroup(
        inputId = "dealer_filter",
        label = "Filter by Dealer:",
        choices = unique(car_data$Dealer),
        selected = unique(car_data$Dealer),
        icon = icon("check"),
        status = "primary",
        inline = TRUE
      ),
      pickerInput(
        inputId = "fuel_filter",
        label = "Filter by Fuel Type:",
        choices = unique(car_data$FuelType),
        selected = unique(car_data$FuelType),
        multiple = TRUE,
        options = list(`actions-box` = TRUE)
      ),
      sliderInput(
        inputId = "price_range",
        label = "Price Range:",
        min = 0,
        max = 55000,
        value = c(0, 55000),
        step = 1000,
        pre = "$"
      )
    )
  ),
  dashboardBody(
    tags$head(tags$style(HTML("
      body, .content-wrapper {
        font-family: 'Roboto', sans-serif;
        background-color: #1C2526;
        color: #E8ECEF;
      }
      .dark-mode {
        background-color: #1C2526 !important;
        color: #E8ECEF !important;
      }
      .box {
        border-radius: 8px;
        border: none;
        background-color: #333333;
        box-shadow: 0px 2px 6px rgba(0,0,0,0.4);
      }
      .box-header {
        background-color: #4682B4;
        color: #E8ECEF;
      }
      .value-box {
        font-size: 18px;
        padding: 15px;
        background-color: #333333 !important;
        color: #E8ECEF !important;
        border: 1px solid #4682B4;
      }
      .toggle-btn {
        float: right;
        margin: 10px;
        background-color: #FF4500;
        color: #E8ECEF;
        border: none;
        border-radius: 5px;
      }
      .toggle-btn:hover {
        background-color: #FF6347;
      }
      .shiny-table th, .shiny-table td {
        color: #E8ECEF;
        border: 1px solid #4682B4;
      }
      .shiny-table th {
        background-color: #4682B4;
      }
      .form-control {
        background-color: #333333;
        color: #E8ECEF;
        border: 1px solid #4682B4;
      }
      .form-control:focus {
        border-color: #FF4500;
        box-shadow: 0 0 5px rgba(255,69,0,0.5);
      }
      .btn-primary {
        background-color: #4682B4;
        border-color: #4682B4;
      }
      .btn-primary:hover {
        background-color: #5A9BD4;
      }
      .error-message {
        color: #FF4500;
        text-align: center;
        padding: 20px;
        font-size: 16px;
      }
    "))),
    tabItems(
      tabItem(tabName = "login",
              fluidRow(
                if (use_shinydashboardPlus && shinydashboardPlus_version >= "2.0.0") {
                  shinydashboardPlus::box(
                    title = "Dealer Login",
                    width = 4,
                    solidHeader = TRUE,
                    status = "primary",
                    closable = FALSE,
                    collapsible = TRUE,
                    textInput("username", "Username:", placeholder = "e.g., dealer1"),
                    passwordInput("password", "Password:", placeholder = "Enter password"),
                    actionButton("login_btn", "Login", icon = icon("sign-in-alt"), class = "btn-primary"),
                    verbatimTextOutput("login_status")
                  )
                } else {
                  shinydashboard::box(
                    title = "Dealer Login",
                    width = 4,
                    solidHeader = TRUE,
                    status = "primary",
                    textInput("username", "Username:", placeholder = "e.g., dealer1"),
                    passwordInput("password", "Password:", placeholder = "Enter password"),
                    actionButton("login_btn", "Login", icon = icon("sign-in-alt"), class = "btn-primary"),
                    verbatimTextOutput("login_status")
                  )
                }
              )
      ),
      tabItem(tabName = "dashboard",
              fluidRow(
                column(12, actionButton("toggle_mode", "Toggle Theme", icon = icon("adjust"), class = "toggle-btn"))
              ),
              fluidRow(
                valueBoxOutput("avgPriceBox", width = 4),
                valueBoxOutput("evCountBox", width = 4),
                valueBoxOutput("hybridCountBox", width = 4)
              ),
              fluidRow(
                if (use_shinydashboardPlus && shinydashboardPlus_version >= "2.0.0") {
                  shinydashboardPlus::box(
                    title = "Eligible Vehicle Prices",
                    width = 6,
                    solidHeader = TRUE,
                    collapsible = TRUE,
                    uiOutput("pricePlotError"),
                    plotlyOutput("pricePlot", height = "400px")
                  )
                } else {
                  shinydashboard::box(
                    title = "Eligible Vehicle Prices",
                    width = 6,
                    solidHeader = TRUE,
                    uiOutput("pricePlotError"),
                    plotlyOutput("pricePlot", height = "400px")
                  )
                },
                if (use_shinydashboardPlus && shinydashboardPlus_version >= "2.0.0") {
                  shinydashboardPlus::box(
                    title = "Vehicle Type Breakdown",
                    width = 6,
                    solidHeader = TRUE,
                    collapsible = TRUE,
                    uiOutput("typePlotError"),
                    plotlyOutput("typePlot", height = "400px")
                  )
                } else {
                  shinydashboard::box(
                    title = "Vehicle Type Breakdown",
                    width = 6,
                    solidHeader = TRUE,
                    uiOutput("typePlotError"),
                    plotlyOutput("typePlot", height = "400px")
                  )
                }
              )
      ),
      tabItem(tabName = "cars",
              fluidRow(
                if (use_shinydashboardPlus && shinydashboardPlus_version >= "2.0.0") {
                  shinydashboardPlus::box(
                    title = "All Eligible Vehicles (Under $55,000)",
                    width = 12,
                    solidHeader = TRUE,
                    collapsible = TRUE,
                    uiOutput("carTableError"),
                    DTOutput("carTable"),
                    downloadButton("download_csv", "Download Filtered Data", class = "btn-primary")
                  )
                } else {
                  shinydashboard::box(
                    title = "All Eligible Vehicles (Under $55,000)",
                    width = 12,
                    solidHeader = TRUE,
                    uiOutput("carTableError"),
                    DTOutput("carTable"),
                    downloadButton("download_csv", "Download Filtered Data", class = "btn-primary")
                  )
                }
              )
      ),
      tabItem(tabName = "about",
              if (use_shinydashboardPlus && shinydashboardPlus_version >= "2.0.0") {
                shinydashboardPlus::box(
                  title = "About the Dashboard",
                  width = 12,
                  solidHeader = TRUE,
                  collapsible = TRUE,
                  p("This advanced R Shiny application enables auto dealers (e.g., Cox Automotive, Autonation, Carvana) to track and market electric and hybrid vehicles under $55,000 eligible for tax deductions. It uses hardcoded data for demo purposes, with dynamic filtering and export options. Built with a robust, masculine design, it’s optimized for demo environments and ready for future API integration.")
                )
              } else {
                shinydashboard::box(
                  title = "About the Dashboard",
                  width = 12,
                  solidHeader = TRUE,
                  p("This advanced R Shiny application enables auto dealers (e.g., Cox Automotive, Autonation, Carvana) to track and market electric and hybrid vehicles under $55,000 eligible for tax deductions. It uses hardcoded data for demo purposes, with dynamic filtering and export options. Built with a robust, masculine design, it’s optimized for demo environments and ready for future API integration.")
                )
              }
      )
    )
  )
)

# Server
server <- function(input, output, session) {
  # Reactive data
  filtered_data <- reactive({
    data <- car_data
    if (!is.data.frame(data)) {
      cat("filtered_data: Input data is not a data frame\n")
      showNotification("Data error: Invalid data format", type = "error")
      return(car_data)
    }
    if (is.null(input$dealer_filter) || is.null(input$fuel_filter) || is.null(input$price_range)) {
      cat("filtered_data: One or more inputs are NULL, returning full data\n")
      return(data)
    }
    filtered <- data[data$Dealer %in% input$dealer_filter &
                       data$FuelType %in% input$fuel_filter &
                       data$Price >= input$price_range[1] &
                       data$Price <= input$price_range[2], ]
    if (!is.data.frame(filtered) || nrow(filtered) == 0) {
      cat("filtered_data: No data matches filters or invalid data, returning full data\n")
      showNotification("No data matches the selected filters; showing all vehicles", type = "warning")
      return(data)
    }
    cat("filtered_data: Returning", nrow(filtered), "rows\n")
    filtered
  })
  
  # Theme toggle
  observeEvent(input$toggle_mode, {
    runjs("
      $('body').toggleClass('dark-mode');
      $('.box').toggleClass('bg-dark text-white');
    ")
  })
  
  # JWT-based login logic (simulated for demo)
  logged_in <- reactiveVal(FALSE)
  observeEvent(input$login_btn, {
    shinyFeedback::feedbackWarning("username", is.null(input$username) || input$username == "", "Enter username")
    shinyFeedback::feedbackWarning("password", is.null(input$password) || input$password == "", "Enter password")
    if (input$username == "" || input$password == "") return()
    
    # Simulate JWT authentication with hardcoded credentials
    if (input$username == "dealer" && input$password == "ev123") {
      session$userData$token <- "mock_jwt_token"
      logged_in(TRUE)
      output$login_status <- renderText("✅ Login successful. Access the dashboard from the sidebar.")
      showNotification("Authenticated", type = "message")
    } else {
      output$login_status <- renderText("❌ Invalid credentials. Try username: dealer, password: ev123")
      logged_in(FALSE)
      showNotification("Invalid credentials", type = "error")
    }
  })
  
  # Restrict access to tabs
  observe({
    if (!logged_in()) {
      hideTab(inputId = "tabs", target = "dashboard")
      hideTab(inputId = "tabs", target = "cars")
    } else {
      showTab(inputId = "tabs", target = "dashboard")
      showTab(inputId = "tabs", target = "cars")
    }
  })
  
  # Value Boxes
  output$avgPriceBox <- renderValueBox({
    data <- filtered_data()
    avg_price <- if (is.data.frame(data) && nrow(data) > 0) round(mean(data$Price), 0) else 0
    valueBox(
      paste0("$", format(avg_price, big.mark = ",")),
      "Avg Vehicle Price",
      icon = icon("dollar-sign"),
      color = "blue"
    )
  })
  
  output$evCountBox <- renderValueBox({
    data <- filtered_data()
    ev_count <- if (is.data.frame(data) && nrow(data) > 0) sum(data$FuelType == "EV") else 0
    valueBox(
      ev_count,
      "EV Models",
      icon = icon("bolt"),
      color = "orange"
    )
  })
  
  output$hybridCountBox <- renderValueBox({
    data <- filtered_data()
    hybrid_count <- if (is.data.frame(data) && nrow(data) > 0) sum(data$FuelType == "Hybrid") else 0
    valueBox(
      hybrid_count,
      "Hybrid Models",
      icon = icon("leaf"),
      color = "black"
    )
  })
  
  # Plotly chart 1: Price by Model
  output$pricePlot <- renderPlotly({
    data <- filtered_data()
    if (!is.data.frame(data)) {
      cat("pricePlot: Data is not a valid data frame\n")
      output$pricePlotError <- renderUI({
        div(class = "error-message", "Error: Invalid data format")
      })
      return(NULL)
    }
    if (nrow(data) == 0) {
      cat("pricePlot: No data available for the selected filters\n")
      output$pricePlotError <- renderUI({
        div(class = "error-message", "No data available for the selected filters")
      })
      return(NULL)
    }
    if (!all(c("Model", "Price", "Dealer", "Make", "Range") %in% colnames(data))) {
      cat("pricePlot: Required columns missing in data\n")
      output$pricePlotError <- renderUI({
        div(class = "error-message", "Required columns missing in data")
      })
      return(NULL)
    }
    output$pricePlotError <- renderUI(NULL)  # Clear error message
    cat("pricePlot: Rendering with", nrow(data), "rows\n")
    plot_ly(
      data = data,
      x = ~Model,
      y = ~Price,
      type = "bar",
      color = ~Dealer,
      colors = c("#4682B4", "#FF4500", "#333333", "#5A9BD4", "#FF6347"),
      text = ~paste("$", format(Price, big.mark = ","), "<br>", Make, "<br>Range:", Range, "mi"),
      textposition = "auto",
      hoverinfo = "text"
    ) %>%
      layout(
        title = list(text = "Car Prices (Max $55K)", font = list(color = "#E8ECEF")),
        xaxis = list(title = "Model", tickangle = 45, titlefont = list(color = "#E8ECEF"), tickfont = list(color = "#E8ECEF")),
        yaxis = list(title = "Price ($)", titlefont = list(color = "#E8ECEF"), tickfont = list(color = "#E8ECEF")),
        plot_bgcolor = "#1C2526",
        paper_bgcolor = "#1C2526",
        showlegend = TRUE
      ) %>%
      config(displayModeBar = FALSE)
  })
  
  # Plotly chart 2: Vehicle Type Breakdown
  output$typePlot <- renderPlotly({
    data <- filtered_data()
    if (!is.data.frame(data)) {
      cat("typePlot: Data is not a valid data frame\n")
      output$typePlotError <- renderUI({
        div(class = "error-message", "Error: Invalid data format")
      })
      return(NULL)
    }
    if (nrow(data) == 0) {
      cat("typePlot: No data available for the selected filters\n")
      output$typePlotError <- renderUI({
        div(class = "error-message", "No data available for the selected filters")
      })
      return(NULL)
    }
    if (!all(c("FuelType", "Price") %in% colnames(data))) {
      cat("typePlot: Required columns missing in data\n")
      output$typePlotError <- renderUI({
        div(class = "error-message", "Required columns missing in data")
      })
      return(NULL)
    }
    output$typePlotError <- renderUI(NULL)  # Clear error message
    cat("typePlot: Rendering with", nrow(data), "rows\n")
    plot_ly(
      data = data,
      labels = ~FuelType,
      values = ~Price,
      type = "pie",
      marker = list(colors = c("#4682B4", "#FF4500")),
      textinfo = "label+percent",
      hoverinfo = "label+value+percent",
      text = ~paste(FuelType, "<br>$", format(Price, big.mark = ","), "<br>Count:", table(FuelType)[FuelType])
    ) %>%
      layout(
        title = list(text = "Fuel Type Distribution", font = list(color = "#E8ECEF")),
        plot_bgcolor = "#1C2526",
        paper_bgcolor = "#1C2526",
        font = list(color = "#E8ECEF"),
        showlegend = TRUE
      ) %>%
      config(displayModeBar = FALSE)
  })
  
  # Data Table
  output$carTable <- renderDT({
    data <- filtered_data()
    if (!is.data.frame(data)) {
      cat("carTable: Data is not a valid data frame\n")
      output$carTableError <- renderUI({
        div(class = "error-message", "Error: Invalid data format")
      })
      return(NULL)
    }
    if (nrow(data) == 0) {
      cat("carTable: No data available for the selected filters\n")
      output$carTableError <- renderUI({
        div(class = "error-message", "No data available for the selected filters")
      })
      return(NULL)
    }
    output$carTableError <- renderUI(NULL)  # Clear error message
    cat("carTable: Rendering with", nrow(data), "rows\n")
    datatable(
      data,
      options = list(
        pageLength = 5,
        autoWidth = TRUE,
        dom = 'Bfrtip',
        buttons = c('copy', 'csv'),
        columnDefs = list(list(className = 'dt-center', targets = '_all'))
      ),
      extensions = "Buttons",
      style = "bootstrap",
      class = "shiny-table",
      rownames = FALSE
    ) %>%
      formatCurrency("Price", "$") %>%
      formatRound("Range", digits = 0)
  })
  
  # CSV Download
  output$download_csv <- downloadHandler(
    filename = function() {
      paste("ev_vehicles_", Sys.Date(), ".csv", sep = "")
    },
    content = function(file) {
      data <- filtered_data()
      if (!is.data.frame(data)) {
        cat("download_csv: Data is not a valid data frame\n")
        showNotification("Error: Invalid data format", type = "error")
        stop("Invalid data format")
      }
      if (nrow(data) == 0) {
        cat("download_csv: No data available to download\n")
        showNotification("No data available to download", type = "error")
        stop("No data available to download")
      }
      cat("download_csv: Exporting", nrow(data), "rows\n")
      write.csv(data, file, row.names = FALSE)
    }
  )
}

# Run the app
shinyApp(ui, server)](#full-code)

Paste this in a new file `app.R` in your RStudio project:

> ⚙️ The full code is already prepared above in your previous message. Due to GitHub formatting limits, **I recommend you copy and paste your existing fully working code block at the bottom of the README file in its own section** as:

```markdown
---

## 📦 Full Code

<copy full app.R code here between fenced code blocks>

```

Let me know and I can generate the Markdown-formatted copy of the code block to paste in directly — or I can help you build a GitHub repo banner as well!
