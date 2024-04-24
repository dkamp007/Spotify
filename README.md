# Spotify

Glad to be sharing my Power BI dashboard of Spotify analysis. The workflow includes:-

## 1. Data cleaning

## 2. Removal of duplicated rows, removing erroneous data points

## 3. Creating Date column for the release date of the songs

## 4. The following DAX measures were created for further analysis:-

      a. Top_song_streams = CALCULATE(SUM([streams]), [streams] = MAX([streams]))

      This measure is used to calculate the sum of all the streams of songs & filters the data to include only rows where the number of streams matches the maximum number of streams in         the entire dataset. Essentially, it identifies the rows corresponding to the top song based on the maximum number of streams.

      b. Avg_stream_per_year = CALCULATE(AVERAGE([streams]), ALLEXCEPT([released_year]))
      
      Calculates the average number of streams & removes all filters from the dataset except for the 'released_year' column to ensure that the average is calculated independently for           each year.

      c. Top_song vs Avg_val = DIVIDE([Top_song_streams] - [Avg_stream_per_year], [Avg_stream_per_year])
      
      This measure calculates the ratio of the difference between the total streams of the top song and the average streams per year to the average streams per year.

      d. Top_song vs avg = 
      
            VAR x = [Top_song vs Avg_val]
            
            RETURN
            
                  IF
                  
                  (x > 0,
                  
                          FORMAT(x, "#.0%") & " " & UNICHAR (9650),
                          
                          FORMAT(x, "#.0%") & " " & UNICHAR (9660))
      
      This measure formats the difference between the top song streams and the average streams per year as a percentage and indicates whether it is an increase or decrease. It checks if        the value of 'x' is greater than zero. If it is, it formats 'x' as a percentage followed by an upward arrow (▲); otherwise, it formats 'x' as a percentage followed by a downward          arrow (▼).

These measures helped compare the performance of the top song with the average streams per year and visualize whether it's above or below average, and by how much.
