## INSTRUCCIONES SQL

categorías eventon:

  SELECT name FROM wp_terms AS t INNER JOIN wp_term_taxonomy AS tt ON t.term_id = tt.term_id AND tt.taxonomy='event_type_2'
