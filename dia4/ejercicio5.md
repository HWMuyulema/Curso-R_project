require(MODISTools)

library(MODISTools) 


??MODISTools  
products <- mt_products()  
head(products)  
bands <- mt_bands(product = "MOD13Q1")  
bands  
dates <- mt_dates(product = "MOD13Q1", lat = -1, lon = -79)  
dates    
subset <- mt_subset(product = "MOD13Q1",   
                    lat = -1,  
                    lon = -79,  
                    band = "250m_16_days_NDVI",  
                    start = "2016-01-01",  
                    end = "2018-12-30",   
                    km_lr = 0,  
                    km_ab = 0,  
                    site_name = "testsite",  
                    internal = TRUE,  
                    progress = FALSE)  
                    
                    
head(subset)  
str(subset)  



date <- as.Date(subset$calendar_date)  
temperature <- subset$value * as.double(subset$scale)  
temperature[temperature == 0] <- NA  



plot(date,  
     temperature,  
     xlab = "Date",  
     ylab = "NDVI",  
     ylim = c(0,1),  
     type = "l")
     
