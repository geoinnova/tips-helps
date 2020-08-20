## INSTRUCCIONES SQL

categorías eventon:

Intervienen: wp_terms y wp_term_taxonomy

  SELECT name, t.term_id FROM wp_terms AS t INNER JOIN wp_term_taxonomy AS tt ON t.term_id = tt.term_id AND tt.taxonomy='event_type_2' 
