
# ---------- 0) Packages ----------
need <- c("tidyverse","Kendall","zyp")
new  <- need[!(need %in% installed.packages()[,1])]
if(length(new)) install.packages(new, repos = "https://cloud.r-project.org")
invisible(lapply(need, library, character.only = TRUE))  


# ---------- 1) Load CSV ----------
csv_path <- "C:\\Users\\shirs\\Downloads\\archive (5)\\long_format_annual_surface_temp.csv"

raw <- readr::read_csv(csv_path, show_col_types = FALSE, guess_max = 100000)

cat("Columns found:\n")
print(names(raw))

# ---------- 2) Clean Year & Temperature ----------
raw <- raw %>%
  mutate(Year = as.numeric(sub("F", "", Year)))

# ---------- 3) Create dat0 ----------
dat0 <- raw %>%
  group_by(Year) %>%
  summarise(Anomaly = mean(Temperature, na.rm = TRUE)) %>%
  filter(Year >= 1961, Year <= 2022)

cat("dat0 rows:", nrow(dat0), "\n")
head(dat0)

# ---------- 4) Remove NA ----------
dat0 <- dat0 %>% filter(!is.na(Anomaly))

# ---------- 5) Baseline adjustment ----------
baseline <- dat0 %>%
  filter(Year >= 1961, Year <= 1990) %>%
  summarise(mean_base = mean(Anomaly, na.rm = TRUE)) %>%
  pull(mean_base)

dat0 <- dat0 %>% mutate(Anomaly = Anomaly - baseline)

# ---------- 6) Mann-Kendall ----------
mk_result <- Kendall::MannKendall(dat0$Anomaly)
print(mk_result)

# Sen's slope result
sen_result <- zyp::zyp.sen(Anomaly ~ Year, dat0)

# Extract coefficients safely
sen_intercept <- unname(coef(sen_result)[1])
sen_slope     <- unname(coef(sen_result)[2])

# Plot with regression + Sen’s slope
ggplot(dat0, aes(x = Year, y = Anomaly)) +
  geom_line(color = "steelblue") +
  geom_point(size = 1, alpha = 0.7) +
  geom_smooth(method = "lm", se = TRUE, color = "red") +  # regression
  geom_abline(intercept = sen_intercept, slope = sen_slope, 
              color = "darkgreen", linewidth = 1, linetype = "dashed") + # Sen's slope
  labs(title = "Global Temperature Anomalies (1961–2022)",
       subtitle = "Red = Linear regression | Green dashed = Sen’s slope",
       y = "Temperature Anomaly (°C)", x = "Year") +
  theme_minimal()


par(mar = c(5, 5, 4, 2))


# ---------- 9) ITA ----------
n <- nrow(dat0)
half <- floor(n/2)

first_half  <- dat0$Anomaly[1:half]
second_half <- dat0$Anomaly[(n-half+1):n]

plot(first_half, second_half,
     xlab = "First half anomalies",
     ylab = "Second half anomalies",
     main = "Innovative Trend Analysis (ITA)")
abline(0, 1, col = "red", lty = 2)
sx8ikl./
