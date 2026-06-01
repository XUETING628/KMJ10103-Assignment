
    setwd('/content/project') # Ensure R working directory is set
    options(scipen = 999) # Prevent scientific notation
    library(qcc)
    library(plotly)
    library(htmlwidgets)
    library(dplyr)

    # Data for Machine 3
    df_machine <- X005 %>% filter(Machine == 3)

    # Ensure data is numeric and sufficient for subgroups
    if (nrow(df_machine) < 5) {
        warning("Not enough data for Machine 3 to create X-bar chart with subgroup size 5. Skipping control chart.")
        # Create a placeholder plot or handle gracefully if no data
        p_machine <- plot_ly() %>%
                      layout(
                        title = list(text = "Not enough data for Control Chart (Machine 3)", font = list(size = 20)),
                        xaxis = list(title = "Observation"),
                        yaxis = list(title = "Part Length")
                      )
    } else {
        df_machine$PartLength <- as.numeric(df_machine$PartLength)

        # Create subgroups for X-bar chart (e.g., every 5 observations)
        subgroup_size <- 5
        num_subgroups <- floor(nrow(df_machine) / subgroup_size)
        df_machine_subgroups <- df_machine[1:(num_subgroups * subgroup_size), ]
        data_matrix_machine <- matrix(df_machine_subgroups$PartLength, ncol = subgroup_size, byrow = TRUE)

        # X-bar chart for PartLength for Machine 3
        qcc_obj_machine <- qcc(data_matrix_machine, type = "xbar", plot = FALSE, ylab = "Part Length")

        # Plotting with plotly for interactivity
        p_machine <- plot_ly(df_machine, x = ~X, y = ~PartLength, type = 'scatter', mode = 'lines+markers', name = 'Part Length') %>%
          add_lines(y = qcc_obj_machine$limits[1], mode = 'lines', name = 'LCL', line = list(color = '#D55E00', dash = 'dash')) %>%
          add_lines(y = qcc_obj_machine$center, mode = 'lines', name = 'Center Line', line = list(color = '#0072B2', dash = 'dash')) %>%
          add_lines(y = qcc_obj_machine$limits[2], mode = 'lines', name = 'UCL', line = list(color = '#D55E00', dash = 'dash')) %>%
          layout(
            title = list(text = 'X-bar Control Chart for Part Length (Machine 3)', font = list(size = 20)),
            xaxis = list(title = list(text = 'Observation', font = list(size = 18)), tickfont = list(size = 14)),
            yaxis = list(title = list(text = 'Part Length', font = list(size = 18)), tickfont = list(size = 14)),
            plot_bgcolor = 'white',
            paper_bgcolor = 'white'
          )
    }

    # Save as HTML widget
    htmlwidgets::saveWidget(as_widget(p_machine), file = "media/plots/plot/control_chart_machine_3.html", selfcontained = TRUE)

