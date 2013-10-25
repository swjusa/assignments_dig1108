```


                            // call the setGravatarImageUrl() method which writes gravatar urls into the session
                            $this->setGravatarImageUrl($result->user_email);


                // call the setGravatarImageUrl() method which writes gravatar urls into the session
                $this->setGravatarImageUrl($result->user_email);



                            // call the setGravatarImageUrl() method which writes gravatar urls into the session
                            $this->setGravatarImageUrl($this->user_email);                

                            $this->errors[] = FEEDBACK_EMAIL_CHANGE_SUCCESSFUL;

                        } else {

                            $this->errors[] = FEEDBACK_UNKNOWN_ERROR;

                        }
                        
                    } else {
                        
                        $this->errors[] = FEEDBACK_PASSWORD_WRONG;
                        
                    }
                    
                }

            } else {

                $this->errors[] = FEEDBACK_EMAIL_DOES_NOT_FIT_PATTERN;

            }  
            
        } elseif (!empty($_POST['user_email'])) {
            
            $this->errors[] = FEEDBACK_PASSWORD_FIELD_EMPTY;
            
        } elseif (!empty($_POST['user_password'])) {
            
            $this->errors[] = FEEDBACK_EMAIL_FIELD_EMPTY;
            
        } else {
            
            $this->errors[] = FEEDBACK_EMAIL_AND_PASSWORD_FIELDS_EMPTY;
            
        }
        
    } 

    public function setGravatarImageUrl($email, $s = 44, $d = 'mm', $r = 'pg', $atts = array() ) {
        
        // TODO: why is this set when it's more a get ?
        
        $url = 'http://www.gravatar.com/avatar/';
        $url .= md5( strtolower( trim( $email ) ) );
        $url .= "?s=$s&d=$d&r=$r";
        
        // the image url (on gravatarr servers), will return in something like
        // http://www.gravatar.com/avatar/205e460b479e2e5b48aec07710c08d50?s=80&d=mm&r=g
        // note: the url does NOT have something like .jpg
        Session::set('user_gravatar_image_url', $url);

        // build img tag around
        $url_with_tag = '<img src="' . $url . '"';
        foreach ( $atts as $key => $val ) {
            $url_with_tag .= ' ' . $key . '="' . $val . '"';
        }
        $url_with_tag .= ' />';            
 
        // the image url like above but with an additional <img src .. /> around
        Session::set('user_gravatar_image_tag', $url_with_tag);
        
    }
    
    /**
     * Gets the user's avatar file path
     * @return string
     */
    