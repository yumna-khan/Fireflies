# issues resolved by Karl Cottenie 
# NOV 12th 2024 

df_fire = vroom::vroom("fireflies_data.tsv")

## _ problem identificatoin -----
df_fire %>% 
  problems() %>% 
  View()
#==> only seem to affect a couple of columns

df_problems = problems(df_fire)$col %>% 
  table()
df_problems
# 12 to be precise

names(df_problems) = names(df_fire)[as.numeric(names(df_problems))]
df_problems

## _ solution 1: increase number of rows to identify column type ------
df_fire %>% 
  problems() %>% 
  group_by(col) %>% 
  summarise(first_row = min(row)) %>% 
  pull(first_row) %>% 
  max()

df_fire2 = vroom::vroom("fireflies_data.tsv", guess_max = 11251)
#end up reading all rows anyway
df_fire2 %>% 
  problems() %>% 
  View()
#==> all the problems are now in column 91

## _ solution 2: remove column 91 from reading into R ----
df_fire3 = vroom::vroom("fireflies_data.tsv", col_select = -c(91))
df_fire3 %>% 
  problems() %>% 
  View()

#==> after forcing vroom to not include column 91, there seems to be no problems anymore

# If you don't need that column, you are ok
