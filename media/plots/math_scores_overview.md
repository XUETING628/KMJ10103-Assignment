# R code for Math scores overview plots
library(ggplot2)
library(dplyr)
library(plotly)
library(patchwork)

# Histogram for Math scores
p1_math <- ggplot(bigclass, aes(x = Math)) +
  geom_histogram(binwidth = 50, fill = "#0072B2", color = "white") +
  labs(title = "Distribution", x = "Math Score", y = "Frequency") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14))

# Boxplot for Math scores by Sex
p2_math <- ggplot(bigclass, aes(x = sex, y = Math, fill = sex)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("M" = "#0072B2", "F" = "#D55E00")) +
  labs(title = "By Sex (Boxplot)", x = "Sex", y = "Math Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "none")

# Bar chart for Average Math scores by Sex
avg_math_by_sex <- bigclass %>% group_by(sex) %>% summarise(AvgMath = mean(Math))
p3_math <- ggplot(avg_math_by_sex, aes(x = sex, y = AvgMath, fill = sex)) +
  geom_bar(stat = "identity", alpha = 0.7) +
  scale_fill_manual(values = c("M" = "#0072B2", "F" = "#D55E00")) +
  labs(title = "Avg. Scores by Sex (Bar)", x = "Sex", y = "Average Math Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "none")

# Scatterplot for Math scores vs. Age
p4_math <- ggplot(bigclass, aes(x = age, y = Math, color = sex)) +
  geom_point(alpha = 0.7, size = 3) +
  scale_color_manual(values = c("M" = "#0072B2", "F" = "#D55E00")) +
  labs(title = "Scores vs. Age (Scatter)", x = "Age", y = "Math Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14))

# Combine plots using patchwork
combined_math_plots <- (p1_math + p2_math) / (p3_math + p4_math) +
  plot_layout(guides = 'collect') +
  plot_annotation(title = "") &
  theme(plot.title = element_text(size = 22, face = "bold"))

# Convert combined plot to plotly
plotly_math_combined <- ggplotly(combined_math_plots)

# Save as HTML widget
htmlwidgets::saveWidget(plotly_math_combined, file = "media/plots/math_scores_overview.html", selfcontained = TRUE)
