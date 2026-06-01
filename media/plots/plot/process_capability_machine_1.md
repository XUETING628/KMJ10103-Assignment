
    setwd('/content/project') # Ensure R working directory is set
    options(scipen = 999) # Prevent scientific notation
    library(qcc)
    library(plotly)
    library(htmlwidgets)
    library(dplyr)

    # Data for Machine 1
    df_machine <- X005 %>% filter(Machine == 1)

    # Ensure data is numeric and sufficient for process capability
    if (nrow(df_machine) < 2) {
        warning("Not enough data for Machine 1 to create Process Capability chart. Skipping.")
        p_pc_machine <- plot_ly() %>%
                        layout(
                          title = list(text = "Not enough data for Process Capability Chart (Machine 1)", font = list(size = 20)),
                          xaxis = list(title = "Part Length"),
                          yaxis = list(title = "Frequency")
                        )
    } else {
        df_machine$PartLength <- as.numeric(df_machine$PartLength)

        # Define specification limits (example values, adjust as needed)
        LSL <- 45 # Lower Specification Limit
        USL <- 55 # Upper Specification Limit

        # Create a qcc object from the data for process.capability
        # Using type="xbar.one" for individual observations
        qcc_data_pc <- qcc(df_machine$PartLength, type = "xbar.one", plot = FALSE)

        # Process capability for PartLength for Machine 1
        pc_obj_machine <- qcc::process.capability(qcc_data_pc, spec.limits = c(LSL, USL))

        # Extract Cp and Cpk values safely and ensure they are numeric
        Cp_value <- as.numeric(pc_obj_machine$overall.capability['Cp', 'Value'])
        Cpk_value <- as.numeric(pc_obj_machine$overall.capability['Cpk', 'Value'])

        # Generate a histogram for PartLength with specification limits
        hist_data_machine <- hist(df_machine$PartLength, plot = FALSE)
        p_pc_machine <- plot_ly(x = hist_data_machine$mids, y = hist_data_machine$counts, type = 'bar', name = 'Frequency') %>%
          add_lines(x = c(LSL, LSL), y = c(0, max(hist_data_machine$counts, 0.1)), name = 'LSL', line = list(color = '#D55E00', dash = 'dash')) %>%
          add_lines(x = c(USL, USL), y = c(0, max(hist_data_machine$counts, 0.1)), name = 'USL', line = list(color = '#D55E00', dash = 'dash')) %>%
          layout(
            title = list(text = paste0('Process Capability for Part Length (Machine 1)<br>LSL: ', LSL, ', USL: ', USL, '<br>Cp: ', round(Cp_value, 2), ', Cpk: ', round(Cpk_value, 2)), font = list(size = 20)),
            xaxis = list(title = list(text = 'Part Length', font = list(size = 18)), tickfont = list(size = 14)),
            yaxis = list(title = list(text = 'Frequency', font = list(size = 18)), tickfont = list(size = 14)),
            plot_bgcolor = 'white',
            paper_bgcolor = 'white'
          )
    }

    # Save as HTML widget
    htmlwidgets::saveWidget(as_widget(p_pc_machine), file = "media/plots/plot/process_capability_machine_1.html", selfcontained = TRUE)

