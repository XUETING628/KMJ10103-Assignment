# R code for Verbal scores overview plots
library(ggplot2)
library(dplyr)
library(plotly)
library(patchwork)

# Histogram for Verbal scores
p1_verbal <- ggplot(bigclass, aes(x = Verbal)) +
  geom_histogram(binwidth = 50, fill = "#009E73", color = "white") +
  labs(title = "Distribution", x = "Verbal Score", y = "Frequency") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14))

# Boxplot for Verbal scores by Sex
p2_verbal <- ggplot(bigclass, aes(x = sex, y = Verbal, fill = sex)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("M" = "#009E73", "F" = "#CC79A7")) +
  labs(title = "By Sex (Boxplot)", x = "Sex", y = "Verbal Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "none")

# Bar chart for Average Verbal scores by Sex
avg_verbal_by_sex <- bigclass %>% group_by(sex) %>% summarise(AvgVerbal = mean(Verbal))
p3_verbal <- ggplot(avg_verbal_by_sex, aes(x = sex, y = AvgVerbal, fill = sex)) +
  geom_bar(stat = "identity", alpha = 0.7) +
  scale_fill_manual(values = c("M" = "#009E73", "F" = "#CC79A7")) +
  labs(title = "Avg. Scores by Sex (Bar)", x = "Sex", y = "Average Verbal Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "none")

# Scatterplot for Verbal scores vs. Age
p4_verbal <- ggplot(bigclass, aes(x = age, y = Verbal, color = sex)) +
  geom_point(alpha = 0.7, size = 3) +
  scale_color_manual(values = c("M" = "#009E73", "F" = "#CC79A7")) +
  labs(title = "Scores vs. Age (Scatter)", x = "Age", y = "Verbal Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14))

# Combine plots using patchwork
combined_verbal_plots <- (p1_verbal + p2_verbal) / (p3_verbal + p4_verbal) +
  plot_layout(guides = 'collect') +
  plot_annotation(title = "") &
  theme(plot.title = element_text(size = 22, face = "bold"))

# Convert combined plot to plotly
plotly_verbal_combined <- ggplotly(combined_verbal_plots)

# Save as HTML widget
htmlwidgets::saveWidget(plotly_verbal_combined, file = "media/plots/verbal_scores_overview.html", selfcontained = TRUE)
