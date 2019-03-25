require(shiny)  
ui<- fluidPage(  
  fluidRow(wellPanel(  
    tags$h1(strong('Pendiente-intercept app')),  
    tags$h3('y= mx + b')  
  )),  
  fluidRow(column(4,wellPanel(  
      sliderInput(inputId ="m",label = "pendiente (m)",  
              value = 1.3, min=-3, max=3, step = 0.1),  
  sliderInput(inputId = "b",label ="Y-Intercept (b)",  
              value = 1.7, min =-2, max =2, step =0.1)  
  )),  
  
  column(8, wellPanel(  
    plotOutput("myplot")  
))  
)  
)  


server<- function(input, output){  
  output$myplot<- renderPlot({  
    x<- seq(from=-3, to=3, by=1)  
    y<- input$m * x + input$b  
    plot(x, y, type='l',ylim = c(-3,3))  
    abline(h=0)  
    abline(v=0)  
  })  
}  

shinyApp(ui=ui, server = server)
